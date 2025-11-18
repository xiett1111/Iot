graph TD
    S0[S0: 待机<br>P1=0, P2=0, AL=0] -->|I2 (水位 >= 50%)| S1
    S1[S1: 泵1运行<br>P1=1, P2=0, AL=0] -->|!I1 (水位 < 10%)| S0
    S1 -->|I3 (水位 >= 75%)| S2
    S2[S2: 泵1&2运行<br>P1=1, P2=1, AL=0] -->|!I2 & I1 (水位 < 50% 且 >= 10%)| S1
    S2 -->|!I2 & !I1 (水位 < 10%)| S0
    S2 -->|I4 (水位 >= 90%)| S3
    S3[S3: 泵1&2&警报运行<br>P1=1, P2=1, AL=1] -->|!I2 & I1 (水位 < 50% 且 >= 10%)| S1
    S3 -->|!I2 & !I1 (水位 < 10%)| S0
    S3 --(I4=0 且 I2=1)--> S3[S3: 泵1&2&警报运行<br>P1=1, P2=1, AL=1]
    
    style S0 fill:#f9f,stroke:#333,stroke-width:2px
    style S1 fill:#bbf,stroke:#333,stroke-width:2px
    style S2 fill:#bfb,stroke:#333,stroke-width:2px
    style S3 fill:#fbb,stroke:#333,stroke-width:2px
