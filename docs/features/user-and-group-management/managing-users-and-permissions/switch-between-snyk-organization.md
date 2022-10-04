# Snyk 조직 간 전환

**snyk.io 에서**

1. 상단 탐색 메뉴의 드롭다운 메뉴에서 원하는 조직을 선택합니다.
2. GitHub 통합을 통해 snyk.io에 프로젝트를 추가하면 현재 선택된 조직에 프로젝트가 추가됩니다.

**Snyk CLI 에서**

1. 기본 조직만 있는 경우 `snyk monitor`를 실행하여 추가하거나 업데이트하는 모든 프로젝트는 자동으로 기본 조직과 연결됩니다.
2. 둘 이상의 조직이 있는 경우 `snyk config set org=ORG_ID`를 실행하여 새로 추가된 프로젝트를 연결해야 하는 조직을 구성할 수 있습니다.
3. If you would like to override this global configuration for individual runs of `snyk monitor`, run `snyk monitor --org=ORG_ID`.
4. `snyk monitor`의 개별 실행에 대해 이 전역 구성을 재정의하려면 `snyk monitor --org=ORG_ID`를 실행하십시오.

기본값은 [계정 설정](https://app.snyk.io/account)에서 현재 선호하는 조직인 \<ORG\_ID>입니다.

자세한 내용은 [CLI에서 사용할 조직을 선택하는 방법 문서](https://support.snyk.io/hc/en-us/articles/360000920738-How-to-select-the-organization-to-use-in-the-CLI)를 참조하십시오.
