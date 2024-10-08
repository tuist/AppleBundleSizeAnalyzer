---
title: "Add dependency"
titleTemplate: ':title | Quick start | Rosalind | Tuist'
description: "Learn how to add Rosalind to your project."
---

# Add dependency

The first step is to add Rosalind as a dependency to your project. The method you choose depends on the type of project you have.

### Swift Package Manager

You can edit your project's `Package.swift` and add `Command` as a dependency:

```swift
import PackageDescription

let package = Package(
  name: "MyProject",
  dependencies: [
    .package(url: "https://github.com/tuist/Rosalind.git", .upToNextMajor(from: "0.1.0")) // [!code ++]
  ],
  targets: [
    .target(name: "MyProject",
            dependencies: ["Rosalind", .product(name: "Rosalind", package: "Rosalind")]), // [!code ++]
  ]
)
```

### Tuist

First, you'll have to add the `Rosalind` package to your project's `Package.swift` file:

```swift
import PackageDescription

let package = Package(
  name: "MyProject",
  dependencies: [
    .package(url: "https://github.com/tuist/Rosalind.git", .upToNextMajor(from: "0.1.0")) // [!code ++]
  ]
)
```

And then declare it as a dependency of one of your project's targets:

::: code-group
```swift [Project.swift]
import ProjectDescription

let project = Project(
    name: "App",
    organizationName: "tuist.io",
    targets: [
        .target(
            name: "App",
            destinations: [.iPhone],
            product: .app,
            bundleId: "io.tuist.app",
            deploymentTargets: .iOS("13.0"),
            infoPlist: .default,
            sources: ["Targets/App/Sources/**"],
            dependencies: [
                .external(name: "Rosalind"),  // [!code ++]
            ]
        ),
    ]
)
```
:::

Make sure you run `tuist install` to fetch the dependencies before you generate the Xcode project.
