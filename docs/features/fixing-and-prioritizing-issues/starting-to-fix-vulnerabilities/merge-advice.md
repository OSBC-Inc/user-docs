# Merge Advice

는 pull request를 병합해도 주요 변경 사항이 발생하지 않을 것이라는 확신을 나타내기 위해 pull request에 표시하는 배지입니다.

## 계산 방법

이 조언은 다른 Snyk 사용자의 pull request에 대해 동일한 변경이 얼마나 잘 수행되었는지를 기준으로 결정됩니다. PR에 대한 테스트가 통과했습니까 아니면 실패했습니까? 변경 사항이 이후에 롤백되었습니까? 성공적으로 병합되었습니까?

## 표시 방법

충분한 데이터가 수집되면 PR에 “Review recommended" 또는 "High chance of success"이라는 조언을 제공하는 배지를 표시합니다.

![](<../../../.gitbook/assets/image (10).png>)

![](<../../../.gitbook/assets/image (17).png>)

신뢰할 수 있는 조언을 제공할 만큼 충분한 데이터를 아직 수집하지 못한 경우 "not enough data"라는 메시지가 표시됩니다. 충분한 데이터를 수집하면 이 배지를 권장 사항으로 자동 업데이트합니다.　따라서 "not enough data"를 표시하는 배지에 나중에 조언이 표시될 수 있습니다.

![](<../../../.gitbook/assets/image (2).png>)

## 유용성

현재 merge advice 배지는 단일 패키지가 업그레이드되는 Yarn 및 npm에만 사용할 수 있습니다. 더 많은 지원이 곧 제공될 예정입니다.

Snyk이 지원하는 모든 소스 제어 통합은 merge advice를 위해 지원됩니다.
