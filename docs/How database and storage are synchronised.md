# How database and storage are synchronised?

Its based on very simple rule.

```mermaid
graph TB
	A2(Created,Modified)-->B1[Content is same?];
	B1-- yes --->X1["Skip"];
	B1-- no --->C1["Write to the DB"];
	
	E1["Conflict check"] -- "Conflicted metadata existed?" --> F1["Conflict resolving"];
	F1 -- "Auto-resolvable" --> G1["Resolve automatically"] --> E2;
	F1 -- "User decision required" -->G2["Resolving dialog"] -- something decided --> E2;
	G2 -- Dismissed --> X2;
	E2["Write back the result(Including update files)"]-->E1;
	
	E1 -- "Consistent" ----> X2;
	X2["Completed"];
	A3(Deleted)---->C1;

	A4[Replication] --> C2["DB updated"];
	C2 -- Created --> RD1["Create new file"];
	C2 -- Modified or deleted --> RD2["Modify"];
	RD2-->E1;

	subgraph storage event
		A2
		A3
	end
	subgraph Repicational event
		A4
	end


```

Modification will be happen so frequently while we're writing articles, we have the option `Batch Database Update`.
This option queues `Write to the DB` till switching opened file or replicating. Then we have less changeset.
And we can see a document history of `write to the DB` and `DB updated` by `Show history`(While we opening the file) or `Pick file to show history`.