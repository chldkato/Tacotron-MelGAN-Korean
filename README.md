# Tacotron + MelGAN Korean TTS

타코트론과 melgan을 합친 한국어 TTS 입니다

logs-melgan 폴더에 970k까지 학습한 melgan 모델이 압축파일로 있습니다

압축을 해제하시고 사용하시면 됩니다

음성에 대한 스펙은 melgan에 맞춰져 있습니다

타코트론은 post-cbhg를 거치지 않기 때문에 빠르게 학습할 수 있습니다

미리 학습한 모델이 있기 때문에 아래의 Inference대로 실행하면 바로 테스트할 수 있습니다

melgan은 학습이 오래걸리기 때문에 따로 적지 않았습니다

새로 학습하시려면 아래의 melgan 학습 관련 링크를 참고하시면 됩니다

### Training

1. **한국어 음성 데이터 다운로드**

    * [KSS](https://www.kaggle.com/bryanpark/korean-single-speaker-speech-dataset)

2. **폴더 내 압축 해제**

   ```
   tacotron-melgan-korean
     |- korean-single-speaker-speech-dataset
         |- 1
         |- 2
         |- 3
         |- 4
         |- transcript.v.1.x.txt
   ```

3. **Preprocess**
   ```
   python tacotron-pre.py
   ```
     * tacotron-pre.py를 열어서 transcript 버전이 맞는지 확인해야 합니다
     * 실행 후 tacotron-train 폴더에 학습 데이터가 생성됩니다

4. **Train**
   ```
   python tacotron-train.py
   ```
     * logs-tacotron에 학습한 모델이 저장됩니다

   재학습 시
   ```
   python tacotron-train.py --restore_step 40000
   ```
     * 저장한 모델에 맞춰서 학습을 시작할 step을 변경하면 됩니다

### Inference
   ```
   python tacotron-eval.py --checkpoint logs-tacotron/model.ckpt-40000
   ```
   * tacotron-eval.py에서 생성할 문장을 정하고 실행하면 output-tacotron에 멜-스펙트로그램이 저장됩니다    
   ```
   python melgan-eval.py --load_dir logs-melgan/ckpt-970k.pt
   ```     
   * melgan-eval.py를 실행하면 output-melgan에 음성과 스펙트로그램이 저장됩니다


윈도우에서 Tacotron 한국어 TTS 학습하기
  * https://chldkato.tistory.com/141
  
Tacotron 정리
  * https://chldkato.tistory.com/143

윈도우에서 MelGAN 학습하기
  * https://chldkato.tistory.com/144

MelGAN 정리
  * https://chldkato.tistory.com/142
