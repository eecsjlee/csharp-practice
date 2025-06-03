# 트러블 슈팅

## WinForms 항목이 Add New Item에 보이지 않는 문제 해결

Visual Studio에서 `Windows Forms` 프로젝트를 만들었는데,  
`Add > New Item` 메뉴에서 **Windows Form (디자이너)** 항목이 보이지 않는 경우가 있습니다.

이 문제는 주로 **프로젝트를 “폴더만 열었을 때(Folder View)” 발생**하며,  
정상적인 `.csproj` 또는 `.sln` 기반으로 열지 않으면 WinForms 관련 항목이 숨겨집니다.

## 증상

- `Forms` 폴더에서 우클릭 → `Add > New Item...` 선택
- 나오는 항목 중에 `Windows Form`이 없음
- "Text File", "C# Class" 등 일반 파일만 보임
- 아래와 같은 경고가 뜰 수도 있음:  
  `"Miscellaneous Files"` 또는 `The file is not contained within a project that supports code parsing`

## 원인

| 항목 | 설명 |
|------|------|
| 폴더 뷰로 열림 | Visual Studio에서 `.csproj` 파일 없이 폴더만 열었을 경우 |
| 프로젝트 구조 인식 안 됨 | 솔루션/프로젝트 정보가 없어 WinForms 템플릿 로딩 실패 |
| Add New Item 항목 제한 | 일반 텍스트/클래스만 추가 가능함 |

## 해결 방법

### 1. `.csproj` 또는 `.sln` 파일을 직접 열기

1. Visual Studio 종료
2. 프로젝트 폴더로 이동
3. 다음 중 하나를 더블 클릭하여 열기:
   - `BookManager.sln` (솔루션)
   - `BookManager.csproj` (C# 프로젝트)

이제 WinForms 항목이 정상적으로 뜹니다.

## 정상이 되면 이렇게 보여야 합니다

- `Solution Explorer`에서 솔루션 이름과 프로젝트 이름이 계층적으로 표시됨
- `Add > New Item...`에 `Windows Form`, `Component`, `User Control` 등 WinForms 관련 항목이 보임
- 빌드 오류 없이 디자이너가 작동함

## VS에서 새로 만들 땐 이렇게 하세요

```plaintext
파일 → 새 프로젝트 → Windows Forms App (.NET)
