```mermaid
stateDiagram-v2
    S0 : 待机<br>P1=0, P2=0, AL=0
    S1 : 泵1运行<br>P1=1, P2=0, AL=0
    S2 : 泵1&2运行<br>P1=1, P2=1, AL=0
    S3 : 泵1&2&警报运行<br>P1=1, P2=1, AL=1

    S0 --> S1 : I2 (水位 >= 50%)
    S1 --> S0 : !I1 (水位 < 10%)
    S1 --> S2 : I3 (水位 >= 75%)
    S2 --> S1 : !I2 & I1 (水位 < 50% 且 >= 10%)
    S2 --> S0 : !I2 & !I1 (水位 < 10%)
    S2 --> S3 : I4 (水位 >= 90%)
    S3 --> S1 : !I2 & I1 (水位 < 50% 且 >= 10%)
    S3 --> S0 : !I2 & !I1 (水位 < 10%)
    S3 --> S3 : I4=0 且 I2=1

    state S0 #f9f
    state S1 #bbf
    state S2 #bfb
    state S3 #fbb
