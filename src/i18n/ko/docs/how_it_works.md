# 🛠 어떻게 동작하는가

Parcel은 **애셋** 트리를 **번들** 트리로 변환합니다. 다른 대부분의 번들러는 근본적으로 JavaScript 애셋에 기반하고 다른 포맷들이 여기에 붙어서 문자열로 JS 파일에 인라인 됩니다. Parcel은 파일형에 구속력이 없어서 어떤 유형의 애셋도 설정없이 작동합니다. Parcel 번들 과정에는 세 단계가 있습니다.

### 1. 애셋 트리 구성

Parcel은 하나의 진입 애셋을 입력으로 받습니다. 진입 애셋은 어느 유형이라도 가능합니다: JS 파일, HTML, CSS, 이미지 등. 다양한 [애셋 유형](asset_types.html)이 Parcel에 정의되어 있습니다. Parcel은 각 유형이 정확히 어떻게 다뤄져야 하는지 알고 있습니다. 애셋이 분석(parse)되면, 애셋의 의존 요소가 추출되고, 최종적인 컴파일 형태로 변환됩니다. 이것이 애셋 트리를 만듭니다.

### 2. 번들 트리 구성

일단 애셋 트리가 만들어지면, 애셋은 번들 트리 안에 놓이게 됩니다. 진입 애셋을 위한 번들이 만들어지고, 코드 분할을 발생시키는 다이나믹 `import()`를 위한 하위 번들이 만들어 집니다.

형제 번들은 다른 유형의 애셋이 임포트 될 때 만들어 집니다. 예를 들자면 CSS 파일을 JavaScript에서 임포트 하는 경우, 대응하는 JavaScript에 대한 형제 번들 안에 위치하게 됩니다.

만약 하나 이상의 번들에서 애셋이 필요하게 되면, 번들 트리 내의 가장 가까운 공통 조상번들로 끌어올려집니다. 이로써 중복 포함되는 일이 없어집니다.

### 3. 패키징

번들 트리가 만들어지고 나면, 각 번들은 [패키저(packager)](packagers.html)에 의해 특정 유형의 파일로 작성됩니다. 브라우저로 로드되는 최종 파일 안에서 각 애셋이 어떻게 합쳐져야 하는지 패키저는 알고 있습니다.