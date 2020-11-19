# Django Comment Migrate

![Build](https://travis-ci.org/starryrbs/django-comment-migrate.svg?branch=master) 
![https://pypi.org/project/django-comment-migrate/](https://img.shields.io/pypi/v/django-comment-migrate)

An app that provides Django model comment migration

English | [简体中文](./README-zh_CN.md) 

## Feature

- Automatic migration model help_text to comment
- Provide a command to migrate the comment of the specified app


## Examples

1. download python package

    ```shell script
    pip install django-comment-migrate
    ```

2. add django_comment_migrate app

    project/project/settings.py
    
    ```python
    INSTALLED_APPS =[
        "django_comment_migrate",
        ...
    ]
    ```

3. add model 

    project/app/model.py
    
    ```python
    from django.db import models
    
    class CommentModel(models.Model):
        no_comment = models.TextField()
        aaa = models.IntegerField(default=0, help_text="test default")
        help_text = models.CharField(max_length=40,
                                     help_text="this is help text")
    
        class Meta:
            app_label = 'tests'
            db_table = 'comment_model'
    ```

4. execute database migrate

    ```shell script
    python manage.py makemigrations
    python manage.py migrate
    ```

Now check the database table, comments have been generated.

## Command

Provides a comment migration command, 
which allows the database to regenerate comments

```shell script
python manage.py migratecomment
```

> The command needs to be executed after all migrations are executed


## Running the tests

1. Install Tox

    ```shell script
    pip install tox
    ```
   
2. Run 

    ```shell script
    tox
    ```

## Supported Database

- MySQL
- Postgres