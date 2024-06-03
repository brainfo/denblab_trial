# For $\beta$ test of Dnbelab and compared with 10x V3

An overview:

```mermaid
flowchart LR;
    subgraph preprocess
    cr_raw[(cellranger raw)]-.->eD[\emptyDrops\];
    dnbe_raw[(dnbelab raw)]-.->eD;
    cr_raw-->cb[\cellBender\];
    dnbe_raw-->cb;
    eD-.->scb[\scrublet\];
    cb-->scb;
    scb-->cr_filter[(cellranger filtered)];
    scb-->dnbe_filter[(dnbelab filtered)]
    end
    subgraph integrate
    cr_filter-->scVI[\scVI\]
    dnbe_filter-->scVI
    end
    subgraph downstream
    scVI-->scanpy["`cell type
    features analysis
    variance analysis`"]
    end
```

## Folder structure

/upstream_stats: reports from cellranger count and dnbelab run  
/h5_input: h5 matrices from calling cell with EmptyDrops or Cellbender + cellranger count or dnbelab run  
/h5_analysis: general qc before and after scrublet

## Next step

integrate matrices from both platforms with scVI