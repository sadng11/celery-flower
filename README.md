# Django celery flower with redis
### this package use:

- django
- celery
- flower
- django celery beat
- django celery results

## How to use:
- first install all dependency with `requirements.txt`
- add `django_celery_beat` to `INSTALLED_APPS` area in project setting
- add `django_celery_results` to `INSTALLED_APPS` area in project setting
- make `app1` in django and add file `tasks` in your files like this
```python
from celery import shared_task
@shared_task
def add(x, y):
    return x + y

```
- add blew code in last of line in setting
```python
from decouple import config
CELERY_BROKER_URL = config('CELERY_BROKER')
CELERY_RESULT_BACKEND = config('CELERY_BACKEND')

CELERY_BEAT_SCHEDULE = {
    "scheduled_task": {
        "task": "app1.tasks.add",
        "schedule": 3.0,
        "args": (10, 10)
    }
}
```
- after that, run `docker-compose up`  
if every thing is good, django , redis and flower run normally

flower run in port `5555`, django run in `8007` and redis in `6379`