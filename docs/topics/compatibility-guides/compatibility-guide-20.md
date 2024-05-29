[//]: # (title: Compatibility guide for Kotlin 2.0)

_[Keeping the Language Modern](kotlin-evolution.md)_ and _[Comfortable Updates](kotlin-evolution.md)_ are among the fundamental principles in
Kotlin Language Design. The former says that constructs which obstruct language evolution should be removed, and the
latter says that this removal should be well-communicated beforehand to make code migration as smooth as possible.

While most of the language changes were already announced through other channels, like updated changelogs or compiler
warnings, this document provides a complete reference for migration from Kotlin 1.9 to Kotlin 2.0.

> The Kotlin K2 compiler is introduced as part of Kotlin 2.0. For information on the benefits of the new compiler, changes
> you might encounter during migration, and how to roll back to the previous compiler, see [K2 compiler migration guide](k2-compiler-migration-guide.md).
>
{type="note"}

## Basic terms

In this document we introduce several kinds of compatibility:

- _source_: source-incompatible change stops code that used to compile fine (without errors or warnings) from compiling
  anymore
- _binary_: two binary artifacts are said to be binary-compatible if interchanging them doesn't lead to loading or
  linkage errors
- _behavioral_: a change is said to be behavioral-incompatible if the same program demonstrates different behavior
  before and after applying the change

Remember that those definitions are given only for pure Kotlin. Compatibility of Kotlin code from the other languages
perspective
(for example, from Java) is out of the scope of this document.

## Language

<!--
### Title

> **Issue**: [KT-NNNNN](https://youtrack.jetbrains.com/issue/KT-NNNNN)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Short summary**:
>
> **Deprecation cycle**:
>
> - 1.6.20: report a warning
> - 1.8.0: raise the warning to an error
-->

### Deprecate use of a synthetic setter on a projected receiver

> **Issue**: [KT-54309](https://youtrack.jetbrains.com/issue/KT-54309)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Short summary**: If you use the synthetic setter of a Java class to assign a type that conflicts with the class's projected type, an error is triggered.
>
> **Deprecation cycle**:
>
> - 1.8.20: report a warning when a synthetic property setter has a projected parameter type in contravariant position making call-site argument types incompatible
> - 2.0.0: raise the warning to an error

### Correct mangling behavior for duplicate function names in a Java subclass

> **Issue**: [KT-56545](https://youtrack.jetbrains.com/issue/KT-56545)
>
> **Component**: Core language
>
> **Incompatible change type**: behavioral
>
> **Deprecation cycle**:
>
> - 2.0.0: use the correct mangling behavior in function invocations. To revert to previous behaviour, use compiler option -XXLanguage:-MangleCallsToJavaMethodsWithValueClasses.

### Correct type approximation algorithm for types with projections for type arguments

> **Issue**: [KT-49404](https://youtrack.jetbrains.com/issue/KT-49404)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 1.8.20: report a warning on problematic calls
> - 2.0.0: raise the warning to an error

### Consistent behavior for properties when accessed before class initialization

> **Issue**: [KT-56408](https://youtrack.jetbrains.com/issue/KT-56408)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: report an error when a property is accessed before initialization in the affected contexts 

### Report error when there's ambiguity in imported classes with the same name

> **Issue**: [KT-57750](https://youtrack.jetbrains.com/issue/KT-57750)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: report an error when resolving a class name that is present in several packages imported with a star import

### Generate Kotlin lambdas via invokedynamic and LambdaMetafactory by default

> **Issue**: [KT-45375](https://youtrack.jetbrains.com/issue/KT-45375)
>
> **Component**: Core language
>
> **Incompatible change type**: behavioral
>
> **Deprecation cycle**:
>
> - 2.0.0: implement new behavior

### Forbid if condition with one branch when an expression is required

> **Issue**: [KT-57871](https://youtrack.jetbrains.com/issue/KT-57871)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: report an error

### Prohibit violation of self upper bounds by passing a star-projection of a generic type

> **Issue**: [KT-61718](https://youtrack.jetbrains.com/issue/KT-61718)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: report an error when self upper bounds are violated by passing a star-projection of a generic type

### Prohibit private inline functions from having a return type that contains an anonymous type

> **Issue**: [KT-54862](https://youtrack.jetbrains.com/issue/KT-54862)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 1.9.0: report a warning on private inline functions if the inferred return type contains an anonymous type
> - 2.0.0: approximate return type of such private inline functions to a supertype

### Change overload resolution behavior to prioritize function calls over invoke conventions

> **Issue**: [KT-37592](https://youtrack.jetbrains.com/issue/KT-37592)
>
> **Component**: Core language
>
> **Incompatible change type**: behavioral
>
> **Short summary**:
>
> **Deprecation cycle**:
>
> - 2.0.0: change overload resolution behavior to consistently prioritize function calls over invoke conventions

### Report error when an inherited member conflict occurs in supertypes from binary dependencies

> **Issue**: [KT-51194](https://youtrack.jetbrains.com/issue/KT-51194)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 1.7.0: report a warning CONFLICTING_INHERITED_MEMBERS_WARNING on declarations where inherited member conflict has occurred in the supertype from binary dependency
> - 2.0.0: raise the warning to an error: CONFLICTING_INHERITED_MEMBERS

### Ignore @UnsafeVariance annotations when reporting errors about type mismatch in contravariant parameters

> **Issue**: [KT-57609](https://youtrack.jetbrains.com/issue/KT-57609)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: implement new behavior

### Report error for out-of-call references to a companion object's member

> **Issue**: [KT-54316](https://youtrack.jetbrains.com/issue/KT-54316)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 1.8.20: report a warning on a companion object function reference type inferred as an unbound reference
> - 2.0.0: change the behavior so that companion object function references are inferred as bound references in all usage contexts

### Require Opt in when calling a constructor that has parameter types that require an Opt in

> **Issue**: [KT-33917](https://youtrack.jetbrains.com/issue/KT-33917)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 1.3.0: report a warning on calls to own members of anonymous objects, returned from private inline functions
> - 2.0.0: approximate return type of such private inline functions to a supertype and don't resolve calls to anonymous object members.

### Report error for an unsound smart cast after a while-loop break

> **Issue**: [KT-22379](https://youtrack.jetbrains.com/issue/KT-22379)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: implement new behavior
>
> The old behavior can be restored by switching to language version 1.9.

### Report error when a variable of an intersection type is assigned a value that is not a subtype of that intersection type

> **Issue**: [KT-53752](https://youtrack.jetbrains.com/issue/KT-53752)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: report an error when a variable having an intersection type is assigned a value that is not a subtype of that intersection type

### Deprecate SAM constructor usages which require OptIn without annotation

> **Issue**: [KT-52628](https://youtrack.jetbrains.com/issue/KT-52628)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 1.7.20: report a warning for OptIn usages via SAM constructor, the warning in this case is never promoted to an error
> - 2.0.0:  raise the warning to an error in K2 compiler for OptIn usages via SAM constructor (or keep reporting the warning if OptIn marker severity is a warning)

### Deprecate upper bound violation in typealias constructors

> **Issue**: [KT-54066](https://youtrack.jetbrains.com/issue/KT-54066)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 1.8.0: introduce a warning, this warning never becomes an error
> - 2.0.0: raise the warning to an error in K2 compiler

### Make the real type of a destructuring variable consistent with the explicit type when specified

> **Issue**: [KT-57011](https://youtrack.jetbrains.com/issue/KT-57011)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Deprecation cycle**:
>
> - 2.0.0: implement new behavior

### Title

> **Issue**: [KT-NNNNN](https://youtrack.jetbrains.com/issue/KT-NNNNN)
>
> **Component**: Core language
>
> **Incompatible change type**: source
>
> **Short summary**:
>
> **Deprecation cycle**:
>
> - 1.6.20: report a warning
> - 1.8.0: raise the warning to an error

### Other language changes {initial-collapse-state="expanded"}

| Issue ID                                                  | Title                                                                                                                          |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| [KT-37592](https://youtrack.jetbrains.com/issue/KT-37592) | Property invoke of a functional type with receiver is preferred over extension function invoke                                 |
| [KT-57609](https://youtrack.jetbrains.com/issue/KT-57609) | K2: Stop relying on the presence of @UnsafeVariance using for contravariant parameters                                         |
| [KT-55111](https://youtrack.jetbrains.com/issue/KT-55111) | OptIn: forbid constructor calls with default arguments under marker                                                            |
| [KT-52802](https://youtrack.jetbrains.com/issue/KT-52802) | Report ambiguity resolving between property/field and enum entry                                                               |
| [KT-58260](https://youtrack.jetbrains.com/issue/KT-58260) | Make invoke convention work consistently with expected desugaring                                                              |
| [KT-55179](https://youtrack.jetbrains.com/issue/KT-55179) | False negative PRIVATE_CLASS_MEMBER_FROM_INLINE on calling private class companion object member from internal inline function |
| [KT-54663](https://youtrack.jetbrains.com/issue/KT-54663) | Projected types don't take into account in-place not null types                                                                |
| [KT-57178](https://youtrack.jetbrains.com/issue/KT-57178) | Change inferred type of prefix increment to return type of getter instead of return type of inc() operator                     |
| [KT-61749](https://youtrack.jetbrains.com/issue/KT-61749) | Forbid unsound bound violation in generic inner class of generic outer class                                                   |
| [KT-64342](https://youtrack.jetbrains.com/issue/KT-64342) | SAM conversion of parameter types of callable references leads to CCE                                                          |
| [KT-64299](https://youtrack.jetbrains.com/issue/KT-64299) | Companion scope is ignored for resolution of annotations on companion object                                                   |
| [KT-47310](https://youtrack.jetbrains.com/issue/KT-47310) | Change qualifier resolution behavior when companion property is preferred against enum entry                                   |
| [KT-41034](https://youtrack.jetbrains.com/issue/KT-41034) | K2: Change evaluation semantics for combination of safe calls and convention operators                                         |
| [KT-58589](https://youtrack.jetbrains.com/issue/KT-58589) | Deprecate missed MUST_BE_INITIALIZED when no primary constructor is presented or when class is local                           |
| [KT-61182](https://youtrack.jetbrains.com/issue/KT-61182) | Unit conversion is accidentally allowed to be used for expressions on variables + invoke resolution                            |
| [KT-62998](https://youtrack.jetbrains.com/issue/KT-62998) | Forbid assignment of a nullable to a not-null Java field as a selector of unsafe assignment                                    |
| [KT-57600](https://youtrack.jetbrains.com/issue/KT-57600) | Forbid overriding of Java method with raw-typed parameter with generic typed parameter                                         |
| [KT-47313](https://youtrack.jetbrains.com/issue/KT-47313) | Change (V)::foo reference resolution when V has a companion                                                                    |
| [KT-54997](https://youtrack.jetbrains.com/issue/KT-54997) | Forbid implicit non-public-API accesses from public-API inline function                                                        |
| [KT-57422](https://youtrack.jetbrains.com/issue/KT-57422) | K2: Prohibit use-site 'get' targeted annotations on property getters                                                           |
| [KT-34372](https://youtrack.jetbrains.com/issue/KT-34372) | Report missed error for virtual inline method in enum classes                                                                  |
| [KT-47986](https://youtrack.jetbrains.com/issue/KT-47986) | Forbid implicit inferring a type variable into an upper bound in the builder inference context                                 |
| [KT-53982](https://youtrack.jetbrains.com/issue/KT-53982) | Keep nullability when approximating local types in public signatures                                                           |
| [KT-65776](https://youtrack.jetbrains.com/issue/KT-65776) | [LC] K2 breaks \`false && ...\` and \`false \|\| ...\`                                                                         |

## Tools

### Visibility changes in Gradle

> **Issue**: [KT-64653](https://youtrack.jetbrains.com/issue/KT-64653)
>
> **Component**: Gradle
>
> **Incompatible change type**: source
>
> **Short summary**: Previously, certain Kotlin DSL functions and properties intended for a specific DSL context would 
> inadvertently leak into other DSL contexts. We've added the `@KotlinGradlePluginDsl` annotation,
> which prevents the exposure of the Kotlin Gradle plugin DSL functions and properties to levels where they are not intended
> to be available. The following levels are separated from each other:
> * Kotlin extension
> * Kotlin target
> * Kotlin compilation
> * Kotlin compilation task
>
> **Deprecation cycle**:
>
> - 2.0.0: for most popular cases, the compiler reports warnings with suggestions on how to fix them if your build script
>   is configured incorrectly; otherwise, the compiler reports an error

### Deprecate `kotlinOptions` DSL

> **Issue**: [KT-63419](https://youtrack.jetbrains.com/issue/KT-63419)
>
> **Component**: Gradle
>
> **Incompatible change type**: source
>
> **Short summary**: The ability to configure compiler options through the `kotlinOptions` DSL and the related
> `KotlinCompile<KotlinOptions>` task interface have been deprecated.
>
> **Deprecation cycle**:
>
> - 2.0.0: report a warning

### Deprecate `compilerOptions` in `KotlinCompilation` DSL

> **Issue**: [KT-65568](https://youtrack.jetbrains.com/issue/KT-65568)
>
> **Component**: Gradle
>
> **Incompatible change type**: source
>
> **Short summary**: The ability to configure the `compilerOptions` property in the `KotlinCompilation` DSL has been deprecated.
>
> **Deprecation cycle**:
>
> - 2.0.0: report a warning

### Deprecate old ways of CInteropProcess handling

> **Issue**: [KT-62795](https://youtrack.jetbrains.com/issue/KT-62795)
>
> **Component**: Gradle
>
> **Incompatible change type**: source
>
> **Short summary**: the `CInteropProcess` task and the `CInteropSettings` class now use the `definitionFile` property
> instead of `defFile` and `defFileProperty`.
> 
> This eliminates the need to add extra `dependsOn` relations between the `CInteropProcess` task and the task that
> generates `defFile` when the `defFile` is dynamically generated.
> 
> In Kotlin/Native projects, Gradle now lazily verifies the presence of the `definitionFile` property after the connected
> task has run later in the build process.
>
> **Deprecation cycle**:
>
> - 2.0.0: `defFile` and `defFileProperty` parameters are deprecated

### Remove kotlin.useK2 Gradle property

> **Issue**: [KT-64379](https://youtrack.jetbrains.com/issue/KT-64379)
>
> **Component**: Gradle
>
> **Incompatible change type**: behavioral
>
> **Short summary**: The `kotlin.useK2` Gradle property has been removed. In Kotlin 1.9.*, it could be used to enable the
> K2 compiler. In Kotlin 2.0.0 and later, the K2 compiler is enabled by default, so the property has no effect
> and cannot be used to switch back to the previous compiler.
>
> **Deprecation cycle**:
>
> - 1.8.20: the `kotlin.useK2` Gradle property is deprecated
> - 2.0.0: the `kotlin.useK2` Gradle property is removed

### Remove deprecated platform plugin IDs

> **Issue**: [KT-65187](https://youtrack.jetbrains.com/issue/KT-65187)
>
> **Component**: Gradle
>
> **Incompatible change type**: source
>
> **Short summary**: support for these platform plugin IDs have been removed:
> * `kotlin-platform-android`
> * `kotlin-platform-jvm`
> * `kotlin-platform-js`
> * `org.jetbrains.kotlin.platform.android`
> * `org.jetbrains.kotlin.platform.jvm`
> * `org.jetbrains.kotlin.platform.js`
>
> **Deprecation cycle**:
>
> - 1.3: the platform plugin IDs are deprecated
> - 2.0.0: the platform plugin IDs are no longer supported