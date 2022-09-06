# setup.py 파일이 스캔에 실패하거나 의존성을 찾지 못하는이유

`snyk test --file=setup.py` command를 실행하면 일반적으로 일부 Python `setup.py` 프로젝트가 실패하거나 의존성을 0개 출력합니다. 이는 Snyk이 나열된 모든 패키지가 포함된 `install_required` 키만 읽기 때문입니다.

다른 필수 키의 의존성은 검색되지 않습니다.

향후 지원은 변경될 수 있습니다.
