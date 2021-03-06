===========
DataReducer
===========

:Info: DataReducer is an python tool for easily handling data.

:Repository: https://github.com/shinrel22/data_reducer

:Author: Tri Nguyen (https://github.com/shinrel22)

:Maintainer: Tri Nguyen (https://github.com/shinrel22)


WARNING
============
THIS REPO IS NO LONGER MAINTENAINCE, PLEASE MOVE TO https://github.com/shinrel22/python_dict_filter

Installation
============

``pipenv install python-data-reducer``

Examples
========
Some simple examples of what DataReducer can do:

.. code :: python

    from data_reducer import DataReducer
    
    >>> origin_data = {
        'id': '1',
        'avatar': {
            'creator': {
                'birthday': {'day': 22, 'month': 1, 'year': 1993},
                'email': 'example@gmail.com',
                'id': '1',
                'name': 'example'
            },
            'deleted': False,
            'id': '1',
            'path': 'abc',
            'types': ['a', 'b', 'c'],
            'url': 'url'
        },
        'translations': [
            {'content': '1', 'id': '1', 'locale': 'vi', 'name': 'A'},
            {'content': '2', 'id': '2', 'locale': 'en', 'name': 'B'}
        ]
    }

    # define fields those you want to keep,
    # use "." to separate nested objects
    >>> only_fields = [
        'id',
        'translations.id',
        'translations.locale',
        'translations.name',
        'translations.types',
        'avatar.url',
        'avatar.id',
        'avatar.creator.id',
        'avatar.creator.birthday.year',
    ]
    
    >>> DataReducer(data=origin_data, include_fields=only_fields).run()
    # your beautiful result
    {
        'id': '1',
        'translations': [
            {'id': '1', 'locale': 'vi', 'name': 'A'},
            {'id': '2', 'locale': 'en', 'name': 'B'}
        ],
        'avatar': {
            'url': 'url',
            'id': '1',
            'creator': {
                'id': '1',
                'birthday': {'year': 1993}
            }
        }
    }
