# CodeCMR

CodeCMR: Cross-Modal Retrieval For Function-Level Binary Source Code Matching (NeurIPS-2020)

## Dependencies

- pandas=0.25.1
- networkx=2.3

## Dataset description

Trainset: 30,000
Validset: 10,000
Testset: 10,000

Each dataset has 33 columns, the first column is the source code, the other columns are the corresponding binary code on 32 combinations of different compilers (gcc/clang), different platforms (x86/x64/arm/arm64) and different optimizations (O0/O1/O2/O3).
Please first download the data from [google cloud](https://drive.google.com/file/d/1Ep74iF6oidV3zmDrAzi1Q4RIwKugpzG4/view?usp=sharing) and uncompress it:
```
7z x all-arch-nx.zip
```

## How to load data

    import pandas as pd
    import networkx as nx

    df = pd.read_pickle('test.pkl')
    print(df.columns)                   # 33 columns

    sample = df.iloc[0]
    src, bin = sample['c_label'], sample['gcc-x64-O0']

    print(src)                          # character-level source code
    g = nx.read_gpickle(bin)
    print(g.graph)                      # binary code literal features, we only use c_int and c_str
    print(g.nodes.data('feat'))         # binary code CFG features


