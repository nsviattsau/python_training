# python_training — UI test automation for the Addressbook web app

Automated tests for the open-source **Addressbook** PHP application (groups and contacts), using the same page helpers across four test styles.

## What is tested

- Create, edit and delete **groups** and **contacts**; add contacts to groups
- Phone numbers, emails and addresses shown on the home page match the edit form
- **UI vs database checks**: data shown in the app is compared with MySQL (direct SQL and Pony ORM)
- Data-driven tests with generated random data (JSON / Python generators)

## Stack

| | |
|---|---|
| UI automation | Selenium WebDriver (Firefox / Chrome) |
| Test runner | PyTest with fixtures, CLI options (`--browser`, `--target`, `--check_ui`) |
| BDD | pytest-bdd (`bdd/*.feature`) |
| Keyword-driven | Robot Framework (`rf/*.robot`) |
| Reporting | Allure |
| Database | PyMySQL, Pony ORM |

Structure follows the **Application / Helper** pattern: `fixture/` (session, group, contact, DB helpers), `model/` (data objects), `generator/` (test data), `test/` (tests).

## Run it

Requires a local Addressbook + MySQL instance; set URLs and credentials in `target.json`.

```bash
pip install -r requirements.txt

pytest test/ --browser=chrome                 # PyTest suite
pytest test/ --check_ui                       # also compare DB results with the UI
pytest bdd/                                   # BDD scenarios
robot -P . rf/group_scenarios.robot rf/entry_scenarios.robot
pytest --alluredir allure-results test-allure/ && allure serve allure-results
```
