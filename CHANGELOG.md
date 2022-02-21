# Changelog

## [1.1.0](https://github.com/extra2000/beats-metricbeat-pod/compare/v1.0.2...v1.1.0) (2022-02-21)


### Features

* **dockerfile:** upgrade Metricbeat from `7.16.2` to `8.0.0` ([f4c89bc](https://github.com/extra2000/beats-metricbeat-pod/commit/f4c89bc74985c5372ff21a0f31fc7a03a64debe5))


### Performance Improvements

* **modules:** reduce check frequency from every 10 seconds to every 300 seconds ([df46671](https://github.com/extra2000/beats-metricbeat-pod/commit/df46671fce4669666664cb80695381c493d60487))

### [1.0.2](https://github.com/extra2000/beats-metricbeat-pod/compare/v1.0.1...v1.0.2) (2022-01-04)


### Code Refactoring

* **modules:** restructure `list` ([29b0beb](https://github.com/extra2000/beats-metricbeat-pod/commit/29b0bebb3e385b71196599dd3f3729695ecc4c29))

### [1.0.1](https://github.com/extra2000/beats-metricbeat-pod/compare/v1.0.0...v1.0.1) (2022-01-02)


### Fixes

* **modules/system:** add `memory`, `network`, and `socket_summary` metricsets ([a665a42](https://github.com/extra2000/beats-metricbeat-pod/commit/a665a42de3f450f6b2eee99f6c886bdcee7b880e))

## 1.0.0 (2021-12-31)


### Features

* initial implementations ([8806a9c](https://github.com/extra2000/beats-metricbeat-pod/commit/8806a9c06e05e6ff3a94577bfb411986c29ec7e9))


### Documentations

* **README:** update `README.md` ([0f7d338](https://github.com/extra2000/beats-metricbeat-pod/commit/0f7d3383ce41b70d72ee3b2c6db4eacf8e1e6982))


### Continuous Integrations

* add AppVeyor with `semantic-release` ([e57e7aa](https://github.com/extra2000/beats-metricbeat-pod/commit/e57e7aa9996f4298a4072dbcc6df5da6e4b5137f))
