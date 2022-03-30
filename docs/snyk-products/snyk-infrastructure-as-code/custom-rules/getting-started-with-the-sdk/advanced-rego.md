# Custom Rego 빌트인

SDK는 테스트 중에 사용할 수 있는 일부 도우미 Rego 함수도 등록합니다.

함수는 다음과 같습니다.

* `hcl2.unmarshal_file`: 파일의 경로를 가져와 HCL2 형식에서 JSON으로 파싱합니다.
* `yaml.unmarshal_file`: 파일의 경로를 가져와 YAML 형식에서 JSON으로 파싱합니다.

이 두 함수는 `lib/testing/main.rego`의 테스트 프레임워크에 의해 사용되며 JSON fixture를 직접 생성할 필요 없이 fixture 파일 경로를 통과할 수 있습니다.
