# ViewBindingKTX

English | [中文](README_ZH.md)

[![](https://www.jitpack.io/v/DylanCaiCoding/ViewBindingKTX.svg)](https://www.jitpack.io/#DylanCaiCoding/ViewBindingKTX) [![](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://github.com/DylanCaiCoding/ViewBindingKtx/blob/master/LICENSE)

[ViewBinding](https://developer.android.com/topic/libraries/view-binding) reduces exceptions caused by id or type errors, which are recommended by both Google officials and Jake Wharton, but it can be a bit cumbersome to use, so this library can **help you use ViewBinding with as little code as possible in any usage scenario**.

## Feature

- Support for the usage of Kotlin and Java
- Support for the usage of reflection and non-reflection
- Support to modify your base class to support ViewBinding
- Support for BaseRecyclerViewAdapterHelper
- Support for Activity, Fragment, Dialog, Adapter
- Support automatic release of binding class instance in Fragment
- Support for custom combination view
- Support for create PopupWindow
- Support for TabLayout to set custom view
- Support for NavigationView to set header view
- Support for DataBinding to automatically set the lifecycle owner

## Gradle

Add it in your root build.gradle at the end of repositories:
```groovy
allprojects {
    repositories {
        // ...
        maven { url 'https://www.jitpack.io' }
    }
}
```

Add dependencies and configurations：

```groovy
android {
    buildFeatures {
        viewBinding true
    }
}

dependencies {
    // The following are optional, please add as needed
    implementation 'com.github.DylanCaiCoding.ViewBindingKTX:viewbinding-ktx:2.1.0'
    implementation 'com.github.DylanCaiCoding.ViewBindingKTX:viewbinding-nonreflection-ktx:2.1.0'
    implementation 'com.github.DylanCaiCoding.ViewBindingKTX:viewbinding-base:2.1.0'
    implementation 'com.github.DylanCaiCoding.ViewBindingKTX:viewbinding-brvah:2.1.0'
}
```

## Usage

:pencil: **[>> Usage documentation <<](https://dylancaicoding.github.io/ViewBindingKTX/#/en/)**

## Sample

Get the binding instance using the Kotlin property delegate：

```kotlin
class MainActivity : AppCompatActivity() {

  private val binding: ActivityMainBinding by binding()

  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    binding.tvHelloWorld.text = "Hello Android!"
  }
}
```

```kotlin
class HomeFragment : Fragment(R.layout.fragment_home) {

  private val binding: FragmentHomeBinding by binding()
  private val childBinding: LayoutChildBinding by binding(Method.INFLATE)
  
  override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
    super.onViewCreated(view, savedInstanceState)
    binding.container.addView(childBinding.root)
  }
}
```

Use in the base class:

```kotlin
class MainActivity : BaseBindingActivity<ActivityMainBinding>() {

  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    binding.tvHelloWorld.text = "Hello Android!"
  }
}
```

```kotlin
class HomeFragment: BaseBindingFragment<FragmentHomeBinding>() {

  override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
    super.onViewCreated(view, savedInstanceState)
    binding.tvHelloWorld.text = "Hello Android!"
  }
}
```

Use in [BaseRecyclerViewAdapterHelper](https://github.com/CymChad/BaseRecyclerViewAdapterHelper)：

```kotlin
class FooAdapter : BaseQuickAdapter<Foo, BaseViewHolder>(R.layout.item_foo) {

  override fun convert(holder: BaseViewHolder, item: Foo) {
    holder.getBinding(ItemFooBinding::bind).apply {
      tvFoo.text = item.value
    }
  }
}
```

See the [usage documentation](https://dylancaicoding.github.io/ViewBindingKTX) for more usage.

## Change log

[Releases](https://github.com/DylanCaiCoding/ViewBindingKTX/releases)

## Author's other libraries

| Library                                                      | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Longan](https://github.com/DylanCaiCoding/Longan)           | Probably the best Kotlin utils library for Android.                                  |
| [LoadingStateView](https://github.com/DylanCaiCoding/LoadingStateView) | Decoupling the code of toolbar or loading status view.       |
| [MMKV-KTX](https://github.com/DylanCaiCoding/MMKV-KTX)       | Use MMKV with property delegates.                                      |
| [Tracker](https://github.com/DylanCaiCoding/Tracker)       | A lightweight tracking framework based on the tracking idea of Buzzvideo.|

## Thanks

Thanks [ViewBindingPropertyDelegate](https://github.com/kirich1409/ViewBindingPropertyDelegate) for providing an idea without reflection

## License

```
Copyright (C) 2020. Dylan Cai

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
