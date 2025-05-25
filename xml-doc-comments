# XML 문서 주석(XML Documentation Comments)

C#에서는 코드에 대한 설명을 XML 형식으로 주석 처리하여, **자동 문서화** 및 **IntelliSense 지원**을 제공할 수 있습니다. 이 방식은 특히 협업, 유지보수, API 문서 생성 시 매우 유용합니다.

## 기본 문법

XML 문서 주석은 `///` 세 개의 슬래시로 시작하며, 일반적으로 클래스, 메서드, 속성, 필드 등에 사용됩니다.

```csharp
/// <summary>
/// 두 수를 더합니다.
/// </summary>
/// <param name="a">첫 번째 정수</param>
/// <param name="b">두 번째 정수</param>
/// <returns>두 정수의 합</returns>
public int Add(int a, int b)
{
    return a + b;
}
```

## 주요 태그

| 태그                   | 설명                |
| -------------------- | ----------------- |
| `<summary>`          | 해당 요소의 간단한 설명을 작성 |
| `<param name="...">` | 메서드의 매개변수 설명      |
| `<returns>`          | 메서드의 반환값 설명       |
| `<remarks>`          | 부가 설명, 참고할 내용     |
| `<example>`          | 사용 예시             |
| `<exception>`        | 예외 정보 설명          |
| `<value>`            | 속성의 값을 설명할 때 사용   |
| `<typeparam>`        | 제네릭 타입 매개변수 설명    |

### 예시

```csharp
/// <summary>
/// 제네릭 리스트에서 최대값을 반환합니다.
/// </summary>
/// <typeparam name="T">비교 가능한 타입</typeparam>
/// <param name="list">입력 리스트</param>
/// <returns>최댓값</returns>
/// <exception cref="ArgumentException">리스트가 비어 있는 경우</exception>
public T Max<T>(List<T> list) where T : IComparable<T>
{
    if (list == null || list.Count == 0)
        throw new ArgumentException("비어있는 리스트입니다.");

    T max = list[0];
    foreach (var item in list)
    {
        if (item.CompareTo(max) > 0)
            max = item;
    }
    return max;
}
```

## 활성화 및 사용

### 1. XML 주석 파일 생성 설정 (Visual Studio)

`*.csproj` 파일에 아래 옵션을 추가하면 컴파일 시 XML 주석 파일이 생성됩니다.

```xml
<PropertyGroup>
  <GenerateDocumentationFile>true</GenerateDocumentationFile>
</PropertyGroup>
```

또는 Visual Studio:

* 프로젝트 → 속성 → 빌드 → "XML 문서 파일" 체크

### 2. IntelliSense에서 활용

XML 주석은 개발 도중 **마우스 오버 시 설명으로 표시되며**, 라이브러리 사용자에게 유용한 정보를 제공합니다.

## 요약

* `///` 슬래시 3개로 시작하는 XML 형식의 주석
* 자동 문서화 및 IntelliSense 지원 목적
* `summary`, `param`, `returns` 등의 태그 사용
* `*.csproj` 설정을 통해 문서 파일 생성 가능
