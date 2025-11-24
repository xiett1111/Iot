stateDiagram-v2
    direction LR
    
    state S0 {
        待机
        Q1=0, Q2=0, Q3=0
    }
    state S1 {
        泵1运行
        Q1=1, Q2=0, Q3=0
    }
    state S2 {
        泵1&2运行
        Q1=1, Q2=1, Q3=0
    }
    state S3 {
        泵1&2&警报运行
        Q1=1, Q2=1, Q3=1
    }

    [*] --> S0 : Reset/Power On

    S0 --> S1 : I2 (水位 >= 50%)
    S1 --> S0 : !I1 (水位 < 10%)
    S1 --> S2 : I3 (水位 >= 75%)

    S2 --> S3 : I4 (水位 >= 90%)
    S2 --> S1 : !I2 & I1 (水位 < 50% 且 >= 10%)
    S2 --> S0 : !I2 & !I1 (水位 < 10%)

    S3 --> S1 : !I2 & I1 (水位 < 50% 且 >= 10%)
    S3 --> S0 : !I2 & !I1 (水位 < 10%)
    S3 --> S3 : I2 & !I4 (水位 >= 50% 且 < 90%)
    
    style S0 fill:#f9f,stroke:#333,stroke-width:2px
    style S1 fill:#bbf,stroke:#333,stroke-width:2px
    style S2 fill:#bfb,stroke:#333,stroke-width:2px
    style S3 fill:#fbb,stroke:#333,stroke-width:2px
