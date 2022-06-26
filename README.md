## ARB Tooling

![ARB Tooling Logo][arb_tooling_logo]

Developed with 💙 by [Raul Mabe][raulmabe_link]

[![style: very good analysis][very_good_analysis_badge]][very_good_analysis_link]
[![License: MIT][license_badge]][license_link]

Dart tool to translate from ARB to CSV and viceversa.

---

## Considerations and restrictions about the CSV file

- **Field delimiter** must be `,`.
- **Key** must be column with index `0`.
- **Description** is mandatory and must be column with index `1`.
- **Base language** must be column with index `2`.
- **eol** is must be `\r\n`.

Check `/example` folder to see the formatted files.

## Installing

If the CLI application is available on [pub](https://pub.dev), activate globally via:

```sh
dart pub global activate arb_tooling
```

Or locally via:

```sh
dart pub global activate --source=path <path to this package>
```

## Example files

A CSV file of the form

|   **key**   |    **description**     |                                  **en**                                  |                                    **es**                                     |
| :---------: | :--------------------: | :----------------------------------------------------------------------: | :---------------------------------------------------------------------------: |
|    hello    |      Hello world       |                               Hello world!                               |                                  Hola mundo!                                  |
| placeholder | Example of placeholder |                               Hello {name}                               |                                  Hola {name}                                  |
|   plural    |   Example of plural    | {number,plural, =0{Sold out} =1{1 spot left} other{{number} spots left}} | {number,plural, =0{Agotadas} =1{1 plaza libre} other{{number} plazas libres}} |
|  endOfLine  | Example of end of line |    Enter it below to verify it.`\r\n`Check your spam folder as well.     |       Introducelo para verificar.`\r\n`Mira la carpeta de spam también.       |

generates the following ARB files

<details>
<summary>
en.arb
</summary>

```json
{
  "@@locale": "en",
  "hello": "Hello world!",
  "@hello": {
    "description": "Hello world"
  },
  "placeholder": "Hello {name}",
  "@placeholder": {
    "description": "Example of placeholder"
  },
  "plural": "{number,plural, =0{Sold out} =1{1 spot left} other{{number} spots left}}",
  "@plural": {
    "description": "Example of plural"
  },
  "endOfLine": "Enter it below to verify it.\nCheck your spam folder as well.",
  "@endOfLine": {
    "description": "Example of end of line"
  }
}
```

</details>

<details>
<summary>
es.arb
</summary>

```json
{
  "@@locale": "es",
  "hello": "Hola mundo!",
  "@hello": {
    "description": "Hello world"
  },
  "placeholder": "Hola {name}",
  "@placeholder": {
    "description": "Example of placeholder"
  },
  "plural": "{number,plural, =0{Agotadas} =1{1 plaza libre} other{{number} plazas libres}}",
  "@plural": {
    "description": "Example of plural"
  },
  "endOfLine": "Introducelo para verificar.\nMira la carpeta de spam también.",
  "@endOfLine": {
    "description": "Example of end of line"
  }
}
```

</details>

This ARB file can then be converted into localization delegates using [intl](https://docs.flutter.dev/development/accessibility-and-localization/internationalization#adding-your-own-localized-messages) or [intl_utils](https://pub.dev/packages/intl_utils).

**Note**
This process can also be reversed via the `to_csv` commmand.

## Usage

```sh
# To CSV command
$ dart ./bin/arb_tooling.dart to_csv -i example/input/arb -o example/output

# From CSV command -> Local file
$ dart ./bin/arb_tooling.dart from_csv -i example/input/csv/translations.csv -o example/output -p app_

# From CSV command -> URL
$ dart ./bin/arb_tooling.dart from_csv -u https://docs.google.com/spreadsheets/d/{sheet_id}/export\?format\=csv\&id\={sheet_id}\&gid\={gid} -o example/output -p app_

# Show CLI version
$ arb_tooling --version

# Show usage help
$ arb_tooling --help
```

## Running Tests with coverage 🧪

To run all unit tests use the following command:

```sh
$ dart pub global activate coverage 1.2.0
$ dart test --coverage=coverage
$ dart pub global run coverage:format_coverage --lcov --in=coverage --out=coverage/lcov.info
```

To view the generated coverage report you can use [lcov](https://github.com/linux-test-project/lcov)
.

```sh
# Generate Coverage Report
$ genhtml coverage/lcov.info -o coverage/

# Open Coverage Report
$ open coverage/index.html
```

---

[license_badge]: https://img.shields.io/badge/license-MIT-blue.svg
[license_link]: https://opensource.org/licenses/MIT
[very_good_analysis_badge]: https://img.shields.io/badge/style-very_good_analysis-B22C89.svg
[very_good_analysis_link]: https://pub.dev/packages/very_good_analysis
[raulmabe_link]: https://raulmabe.dev
[arb_tooling_logo]: logo.png
