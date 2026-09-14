# Local Code Architecture Analyzer

> A local-first code analysis tool that visualizes class relationships, dependencies, and project architecture.

소스 코드를 외부 AI나 서버로 전송하지 않고 **로컬에서 직접 분석**하여 클래스 구조와 의존성 관계를 시각화하는 개발자용 데스크톱 프로그램입니다.

현재는 **C# / Unity 프로젝트 분석을 중심으로 개발**하며, 향후 다양한 프로그래밍 언어로 확장할 수 있도록 설계합니다.

---

## Features

### Code Analysis

* C# Syntax / Semantic Analysis
* Class / Interface / Struct / Enum 분석
* Inheritance 분석
* Interface Implementation 분석
* Field / Property Reference 분석
* Method / Parameter / Return Type 분석
* Generic Type 분석
* Event / Delegate 분석
* Attribute 분석

### Dependency Analysis

* Dependency Graph
* Incoming / Outgoing Dependencies
* Dependency Depth
* Circular Dependency Detection
* Dependency Count
* Inheritance Depth
* Namespace / Module Dependency

### Visualization

* Class Diagram
* Dependency Graph
* 관계 종류별 시각적 구분
* Pan / Zoom
* Node Drag
* Auto Layout
* Focus Selected
* Collapse / Expand
* Filtering
* Dependency Depth 제한
* Graph Legend

### Unity Support

Unity 프로젝트를 고려하여 다음 요소를 분석합니다.

* `MonoBehaviour`
* `ScriptableObject`
* `SerializeField`
* `SerializeReference`
* `UnityEvent`
* `GetComponent<T>()`
* `GetComponentInChildren<T>()`
* `GetComponentInParent<T>()`
* `Instantiate<T>()`
* `Resources.Load<T>()`
* Assembly Definition

---

## Privacy First

이 프로젝트의 핵심 원칙은 **소스 코드 분석을 로컬에서 수행하는 것**입니다.

```text
Source Code
     ↓
Local Parser
     ↓
Semantic Analysis
     ↓
Dependency Extraction
     ↓
Graph Model
     ↓
Visualization
```

소스 코드 및 분석 결과를 외부 AI / LLM / API로 전송하지 않습니다.

인터넷 연결 없이도 기본적인 코드 분석과 그래프 생성을 수행할 수 있도록 설계합니다.

---

## Screenshots

> Screenshots will be added as the project UI is implemented.

### Dependency Graph

![Dependency Graph](docs/images/dependency-graph.png)

### Class Diagram

![Class Diagram](docs/images/class-diagram.png)

### Architecture View

![Architecture View](docs/images/architecture.png)

---

## Architecture

분석 엔진과 UI를 분리하여 분석 결과를 다양한 형태로 활용할 수 있도록 설계합니다.

```text
┌─────────────────────┐
│         UI          │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│    Application      │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│    Analysis Core    │
│                     │
│ Language Analyzer   │
│ Dependency Analyzer │
│ Architecture        │
│ Analyzer            │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│    Domain Model     │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│     Graph Model     │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│   Graph Renderer     │
└─────────────────────┘
```

### C# Analysis

C# 분석은 Microsoft Roslyn을 기반으로 Syntax Tree와 Semantic Model을 활용합니다.

```text
C# Source
    ↓
Roslyn Compilation
    ↓
Syntax Tree
    ↓
Semantic Model
    ↓
Symbols
    ↓
Relationship Extraction
    ↓
Common Code Model
```

정규식이나 단순 문자열 검색을 핵심 분석 방법으로 사용하지 않습니다.

---

## Supported Languages

| Language        | Parser  | Semantic Analysis | Status         |
| --------------- | ------- | ----------------- | -------------- |
| C#              | Roslyn  | Yes               | In Development |
| C++             | Planned | Planned           | Planned        |
| Java            | Planned | Planned           | Planned        |
| Other Languages | Planned | Planned           | Planned        |

언어별 분석 결과는 공통 Code Model로 변환하여 Dependency Analysis와 Visualization에서 재사용할 수 있도록 설계합니다.

---

## Installation

### Requirements

* Windows
* .NET Runtime / SDK
* 지원되는 운영체제 환경

### From Release

1. [Releases](../../releases)에서 최신 버전을 다운로드합니다.
2. 압축을 해제합니다.
3. 실행 파일을 실행합니다.

### From Source

```bash
git clone https://github.com/your-name/local-code-architecture-analyzer.git
cd local-code-architecture-analyzer
dotnet restore
dotnet build
dotnet run
```

---

## Usage

1. 프로그램을 실행합니다.
2. 분석할 프로젝트 폴더를 Drag & Drop합니다.
3. 소스 코드 분석이 완료될 때까지 기다립니다.
4. Dependency Graph 또는 Class Diagram을 확인합니다.
5. 클래스를 선택하여 관련 Dependency를 확인합니다.
6. Search / Filter / Dependency Depth를 사용하여 필요한 관계만 확인합니다.

---

## Example

다음과 같은 코드가 있다면:

```csharp
public class PlayerController : MonoBehaviour
{
    private WeaponSystem weaponSystem;
    private InventorySystem inventorySystem;

    public void Attack(WeaponSystem weapon)
    {
    }
}
```

분석 결과는 다음과 같은 관계로 표현됩니다.

```text
PlayerController
 ├── Inheritance ──────→ MonoBehaviour
 ├── Field Reference ──→ WeaponSystem
 ├── Field Reference ──→ InventorySystem
 └── Parameter ────────→ WeaponSystem
```

각 관계는 그래프에서 서로 다른 스타일로 표시됩니다.

---

## Development

개발은 다음 단계로 진행합니다.

* [x] 프로젝트 구조 설계
* [ ] C# Source Analysis
* [ ] Dependency Model
* [ ] Dependency Graph
* [ ] Graph UI
* [ ] Class Diagram
* [ ] Search / Filter
* [ ] Circular Dependency Detection
* [ ] Unity-specific Analysis
* [ ] Incremental Analysis
* [ ] Export
* [ ] Additional Language Support

---

## Testing

분석 정확성을 검증하기 위해 다음과 같은 테스트 코드를 사용합니다.

* Inheritance
* Interface
* Multiple Interfaces
* Generic
* Partial Class
* Nested Type
* Namespace
* Circular Dependency
* MonoBehaviour
* ScriptableObject
* SerializeField
* UnityEvent
* Invalid C# Code
* Unresolved Symbols
* Large Projects

핵심 분석 로직은 자동화된 테스트를 통해 검증합니다.

---

## Troubleshooting

### Analysis fails on a single file

하나의 파일에서 오류가 발생하더라도 가능한 다른 파일의 분석은 계속 진행하도록 설계합니다.

문제가 발생한 파일은 Diagnostic 정보와 함께 기록합니다.

### Large graphs become difficult to read

대규모 프로젝트에서는 모든 관계를 동시에 표시하지 않고 다음 기능을 사용합니다.

* Dependency Depth
* Filtering
* Focus Mode
* Collapse / Expand
* Namespace Grouping
* Auto Layout

---

## Roadmap

### Analysis

* [ ] C# Semantic Analysis 개선
* [ ] Assembly Definition 분석
* [ ] Unity API 분석 확대
* [ ] 추가 언어 지원

### Visualization

* [ ] 대규모 Graph 최적화
* [ ] Semantic Zoom
* [ ] Namespace / Assembly Grouping
* [ ] 개선된 Auto Layout

### Developer Tools

* [ ] JSON Export
* [ ] SVG / PNG Export
* [ ] HTML Report
* [ ] Markdown Report
* [ ] CLI
* [ ] Unity Editor Integration

---

## Contributing

Issue와 Pull Request를 환영합니다.

새로운 언어 또는 분석 기능을 추가할 경우 기존 Analysis Core와 Visualization 계층을 최대한 변경하지 않고 확장할 수 있는 구조를 우선합니다.

---

## License

License will be added before the first public release.
