# kddockwidgets_qt6_vendor

ROS 2 vendor package that builds and installs [KDDockWidgets](https://github.com/KDAB/KDDockWidgets) (Qt 6).

## Build Configuration

Vendor build options are centralized in:

- `cmake/kddockwidgets_qt6_vendor-build-options.cmake`

Key settings include:

- Qt 6 build enabled.
- Frontends explicitly set to both `qtwidgets;qtquick`.
- Examples, tests, docs, and Python bindings disabled for the vendor build.

## License

This repository includes the Apache License 2.0 text in [LICENSE](LICENSE).

Note: the vendored upstream project, KDDockWidgets, is dual licensed under GPL-2.0-only or GPL-3.0-only.
