# Snyk에서 발견한 Issue에 대해 Pull Request/Merge Request를 생성할 수 없는 이유는 무엇입니까?

Source Control tool에서 프로젝트를 가져오거나 스캔을 실행할 때마다 프로젝트에 대한 PR 수정 버튼은 반드시 표시되는 것은 아닙니다. Snyk은 직접 의존성에 대해서만 PR을 생성합니다.

프로젝트에 취약점이 포함된 전이 의존성이 있는 경우 Snyk은 취약점에 대해 PR을 생성하지 않습니다.
