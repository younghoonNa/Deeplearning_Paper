# Attention is All You Need

## Abstract 
- sequence transduction 모델은 encoder와 decoder가 포함된 CNN/RNN 기반의 Neural Network가 우세함.
- 최고의 성능을 내는 모델은 Encoder와 Decoder를 통과 후 attention mechanism을 적용한 모델임.
- 이번 논문에서 제안하는 simple network 구조인 트랜스포머는 오로지 attention mechanism 기반으로 전체를 recurrence와 convolutions로 나눔.
- 2개의 실험을 통해 우리의 architecture가 parallelizable(병렬? 병렬 압축 가능?)하며 학습 시 소요 시간이 중요하게 줄어들었다는 것을 보여줄 것.
- WMT 2014 English-German 번역 task에서 28.4 BELU로 이전 최고 기록보다 2BELU 높음. (앙상블 포함)
- WMT 2014 English-French 번역 task에서는 41.9 BELU Score를 기록
- 우리는 제한된 학습 데이터와 "English" 구분 번역에 성공적으로 적용하여 트랜스포머가 일반화가 잘 된다는 것을 보여줌.

