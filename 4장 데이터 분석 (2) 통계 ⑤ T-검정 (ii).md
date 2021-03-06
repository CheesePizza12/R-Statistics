## 4장 데이터 분석 (2) 통계 ⑤ T-검정 (ii)

​

​

#### 2) 두 집단의 평균 검정 - 독립 표본인 경우

(비율을 검정하는 경우 순서는 같고, 통계량 비교하는 부분만 다릅니다)

​     

먼저 독립 표본부터 설명하겠습니다. 독립표본은 2집단이 같지 않은 경우를 의미합니다. 예를 들면 남성과 여성, 학생과 비학생과 같이 2집단에 공통되는 속성이 없는 경우가 이에 해당합니다.

​

반대로 2집단이 같은 경우도 있는데 이를 대응표본이라고 합니다. 조사 이전에 특정 집단을 측정하고, 조사 이후에 같은 집단을 다시 측정하면, 2집단의 속성은 실험이라는 변수를 제외하면 같습니다.

세부적인 내용은 4장 데이터 분석 (2) 통계 ① 통계 기본 개념에 실험을 설명한 부분을 참고하기 바랍니다. 

​     

여기서는 독립표본인 경우의 T-검정을 살펴보겠습니다.

​     

① T-검정에 대한 가설 설정 : 영가설과 대립가설(대안가설)을 세웁니다.

영가설 :   ![t 1](https://user-images.githubusercontent.com/43332543/47087322-a5792300-d256-11e8-8b2b-1611e31a1c18.jpg)  (A집단과 B집단의 모수는 같다) →  ![t 2](https://user-images.githubusercontent.com/43332543/47087323-a611b980-d256-11e8-89d9-1bf5ed8c642a.jpg) 도 가능

대안가설 :  ![t 1](https://user-images.githubusercontent.com/43332543/47087361-bcb81080-d256-11e8-8c65-ae1c93d0ecff.jpg)  (A집단과 B집단의 모수는 다르다) →  ![t 2](https://user-images.githubusercontent.com/43332543/47087362-bcb81080-d256-11e8-854c-a3304938b9a2.jpg) 도 가능

​     

② 정규성 검정 및 등분산성 검정 실시

​     

i) **정규성 검정**(shapiro.test, lillie.test 등)

​     

영가설 : 2개의 모집단이 모두 정규분포를 따른다.

대안가설 : 하나의 모집단이라도 정규분포를 따르지 않는다.

​     

단일표본과 마찬가지로 2집단의 종속변수 각각에 정규성 검정을 실시해 2집단이 모두 정규분포를 따르는 경우와 1집단이라도 정규분포를 따르지 않는 경우로 결과가 나뉩니다.

**p-value가 0.05보다 커야 정규분포를 따른다**는 점을 기억하시기 바랍니다. 여기서는 두 집단 모두 정규분포를 따른다는 전제하에 나머지 검정들을 실시합니다.

​     

ii) **등분산성 검정**(var.test() → var.equal=T or F)

​     

등분산성 검정의 결과에 따라 T-검증의 결과가 달라지는 경우는 드뭅니다. 하지만 정규성 검정에 비해 등분산성 검정은 필수로 실시할 것을 권장합니다.

등분산성 검정은 일반적으로 Levenu의 등분산성을 자주 이용합니다. 앞서 정규성 검정에서 대안가설일 경우(즉, 1집단이라도 정규분포가 아닌 경우) 등분산성 검정을 할 필요는 없습니다.

​     

가) 가설 설정

영가설 : 두 모집단의 분산은 같다( ![default](https://user-images.githubusercontent.com/43332543/47087386-d0fc0d80-d256-11e8-9d8a-8252d589bdcc.jpg) )

대안가설 : 두 모집단의 분산은 다르다( ![default](https://user-images.githubusercontent.com/43332543/47087390-d22d3a80-d256-11e8-8e8e-cb291e33dffd.jpg) )

​     

나) 관찰 F통계량을 구한 다음, 기준 F통계량과 비교하거나 유의확률을 유의수준과 비교

등분산성 검정에서는 F분포를 이용해 F통계량을 구합니다. 앞서 카이제곱 검정과 마찬가지로 통계량을 비교하거나 확률을 비교합니다.

등분산성 검정은 양측검정이므로 F통계량을 이용해 비교하는 경우, 기준 F통계량은 F분포표에서 유의수준과 두 집단의 자유도가 교차하는 셀의 값입니다.

​     

<아래 사이트에서 F분포표를 볼 수 있습니다>

http://math7.tistory.com/60

​     

유의확률을 이용하면 관찰 F통계량이 얼마나 특이한지 나타내는 확률이므로 0.05보다 큰지 작은지만 확인하면 됩니다. p-value만 보면 되므로 통계량을 비교하는 것보다 간편합니다.

​     

다) 등분산성 검정의 가설 검증

**p-value가 0.05보다 작거나** 절댓값 기호를 씌운 관찰 F통계량이 절댓값 기호를 씌운 기준 F통계량보다 큰 경우 영가설을 기각하고 대안가설을 채택합니다. 즉, **두 집단의 분산이 다르므로** R에서는 var.equal=F를 추가하고 SPSS에서는 T검정 결과표의 ‘등분산이 가정되지 않음’ 행을 봐야 합니다.

​     

반대로 p-value가 0.05보다 크거나 절댓값 기호를 씌운 관찰 F통계량이 절댓값 기호를 씌운 기준 F통계량보다 작은 경우는 영가설을 채택합니다. 즉, 두 집단의 분산이 같으므로 R에서는 var.equal=T 인자를 추가하거나(기본값이므로 생략해도 됨) SPSS에서는 T검정 결과표의 ‘등분산이 가정됨’ 행을 봐야 합니다.

​     

③ 관찰 T통계량을 구하고 기준 T통계량과 비교하거나 p-value와 유의수준 비교하기(t.test, welch t-test)

​     

→ T검정의 가설 설정은 ①에서 설정했기 때문에 생략합니다.

​     

두 집단의 평균 차이를 알려면  ![default](https://user-images.githubusercontent.com/43332543/47087413-e5400a80-d256-11e8-96a8-4ed3ca7b7c78.jpg) 의 통계량을 구해 α영역에   ![default](https://user-images.githubusercontent.com/43332543/47087413-e5400a80-d256-11e8-96a8-4ed3ca7b7c78.jpg)  값이 속하면 0과 다르다고 취급하며, α영역이 아닌 곳에 위치하면 0과 같다고 인식하면 됩니다.

그런데 우리는 모수의 평균을 알 수 없기 때문에 표본의 평균으로 모수를 추정해야 합니다. 즉, α영역에 관찰 T통계량이 위치하면 영가설을 기각하고 대안가설을 채택하며, α영역에 T통계량이 위치하지 않으면 영가설을 채택합니다.

​     

위 방식은 T통계량을 이용한 방법이므로   ![t](https://user-images.githubusercontent.com/43332543/47087441-f426bd00-d256-11e8-92c8-2769767e9e76.jpg)  를 직접 구해야 하고, 관찰 T통계량과 T분포표를 이용해 기준 T통계량을 구해야 하므로 다소 불편합니다.

​     

<T분포표는 아래 사이트에서 볼 수 있습니다>

http://math7.tistory.com/56

​     

그래서 p-value(유의확률)을 이용해 T검증이 유의한지, 유의하지 않은지 확인할 수 있습니다. 유의확률이 유의수준보다 작으면 대안가설을 채택하고, 유의확률이 유의수준보다 크면 귀무가설을 채택합니다.

​     

카이제곱 검정에서와 마찬가지로 아래에 정리했습니다.

​     

**관찰 t > 기대 t   =   p-value < 유의수준   =   귀무가설 기각하고 대안가설 채택**

**관찰 t < 기대 t   =   p-value > 유의수준   =   대안가설 기각하고 귀무가설 채택**

​     

​     

④ 두 집단이 정규분포를 따르지 않는 경우의 T검정(wilcox.test)

​     

①의 정규성 검정에서 대안가설을 따라야 하는 경우, ② 등분산성 검정과 ③의 T검정을 하지 말고 바로 wilcox.test를 실시하면 됩니다. wilcox.test도 2집단의 수치 차이를 검증하는 방법이지만, T검정과 다른 공식을 사용해 통계량과 유의확률을 구해준다고 이해하면 됩니다.

구체적인 가설검정이나 가설채택의 방식은 t.test와 같습니다.

​     

참고로 wilcox.test는 윌콕슨 검정, 윌콕슨 순위합 검정, 맨-휘트니 U검정과 같이 다양하게 불리지만, 모두 같은 방법을 나타냅니다.

​     

⑤ 분석/결론

통계적으로 유의수준(신뢰도) O% 하에서 영가설을 채택/기각해 ‘두 집단의 통계량은 같다/다르다’.

또한 A집단의 평균이 B집단의 평균보다 높다/낮다.(집단별 평균을 구해 확인)

​

​

#### 참고문헌

​     

C강사님의 강의노트

L교수님의 통계수업

​     

이종익, 박민석 편저, 「사회조사분석사 2급 필기」, 시대고시기획, 2014.

최용석, 「R과 함께하는 통계학의 이해」, BigBook, 2014.



--2018.10.17