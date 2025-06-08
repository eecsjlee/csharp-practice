# 파일 복사 설정 (CopyToOutputDirectory)

이 문서는 C# 프로젝트 파일(.csproj)에서 설정 파일(JSON 등)을 실행 파일과 함께 빌드 디렉터리로 복사하는 방법을 설명합니다.

## 왜 필요한가요?

C# 프로젝트에서 `.json`, `.txt`, `.png` 같은 일반 파일들은 **기본적으로 빌드 결과물에 포함되지 않습니다**.  
하지만 프로그램 실행 시 이 파일들이 필요하다면, **수동으로 복사**되도록 `.csproj`에 지시해야 합니다.

예:  
- `colors.json` 파일을 `Console.ReadAllText()`로 읽고 싶은 경우
- 리소스 파일, 설정 파일, 사용자 정의 데이터 파일 등

## 실습 예시: `colors.json` 자동 복사

### 프로젝트 구조

```
ConsoleTetris/
├─ Configs/
│  └─ colors.json         ← 복사 대상 파일
└─ ConsoleTetris.csproj   ← 복사 설정 포함
```

## .csproj 설정

```xml
<ItemGroup>
  <None Update="Configs\colors.json">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </None>
</ItemGroup>
```

### 구성 요소 설명

| 태그                        | 의미                |
| ------------------------- | ----------------- |
| `<ItemGroup>`             | 여러 항목 묶음          |
| `<None>`                  | 일반 파일 (컴파일 대상 아님) |
| `Update="..."`            | 기존 파일의 속성을 수정     |
| `<CopyToOutputDirectory>` | 실행 파일과 함께 복사할지 설정 |

## CopyToOutputDirectory 옵션

| 값                  | 설명                             |
| ------------------ | ------------------------------ |
| `Never`            | 복사 안 함 (기본값)                   |
| `Always`           | 항상 복사 (변경 여부 무시)               |
| ✅ `PreserveNewest` | **파일이 변경된 경우만 복사** (가장 많이 사용됨) |

## 빌드 후 결과

```
bin/
└─ Debug/
   └─ net8.0/
      └─ Configs/
         └─ colors.json  ✅ ← 자동 복사 완료
```

## 경로 주의

* 코드에서는 `Path.Combine("Configs", "colors.json")`처럼 경로를 명확히 지정해야 함
* 경로가 다르면 `FileNotFoundException` 또는 `"파일을 찾을 수 없습니다."` 메시지 발생 가능

## 응용 아이디어

* 설정 파일: `appsettings.json`, `colors.json`
* 사용자 데이터: `questions.json`, `data.csv`
* 다국어 리소스: `strings.ko.json`, `strings.en.json`

## 관련 링크

* [.NET SDK MSBuild Items - None](https://learn.microsoft.com/en-us/visualstudio/msbuild/common-msbuild-project-items?view=vs-2022)
* [MSBuild CopyToOutputDirectory 설명](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-common-properties?view=vs-2022)

이 설정을 통해 .csproj 파일로 실행 환경을 자동 구성할 수 있습니다.
덕분에 테스트, 배포, 유지보수 모두 훨씬 더 편리해집니다.
