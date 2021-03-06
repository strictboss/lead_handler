# Lead Handler
Example of using PHP Parallel custom workers pool to process lots of synthetic leads with long in time handling.
"Hard" handling of each lead is simulated with `sleep(2);`.
Result of handling all leads you can see in `log.txt` file, when script completed.

**To start project:**
1. Clone repository: `git clone https://github.com/dimon17/lead_handler.git`
2. Cd into the directory: `cd lead_handler`
3. Install dependencies: `composer install` (or, if you do not have installed composer locally, change for first run `command` property of `php_cli` service in `docker-compose.yml` file to `bash -c "composer install && php LetsRoll.php"`; after executing point 4, when Docker image will be built, dependencies will be installed and script will be executed - return value of the property to `php LetsRoll.php`)
4. Run project: `docker-compose up`
5. Enjoy! :)

**Configuration:**
1. Allowed leads categories to process enumerated in two configuration files `src/Config/App/scripts/leadsAllowedCategoriesProd.php` and `src/Config/App/scripts/leadsAllowedCategoriesDev.php`. It can be changed while runtime (one remark: it must be valid by PHP syntax). Only one of these two files is used by the project while run.
2. You can specify your own configuration file in `LetsRoll.php` script, or change value of environment variable `DEV` in `docker-compose.yml` (values 0 and 1 are allowed). Number of synthetic leads and workers in pool specified in configuration files `src/Config/App/Prod.php` and `src/Config/App/Dev.php`.
3. Workers bootstrap files are placed by the path `src/Tools/WorkersPoolParallel/WorkerBootstrap/scripts/`, but each of them shall be described in class-files, placed at high level directory, and class shall implement `IWorkerBootstrap` interface.

Unfortunately, PHP Parallel module has ~~a lot of pain with memory usage (leaks, etc.)~~ lots of opened issues on Github - https://github.com/krakjoe/parallel/issues (it is 36 now), but i believe, author ~~will create new broken fork~~ will continue working on this excellent tool, and it will be finished soon.