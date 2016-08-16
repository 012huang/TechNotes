---
title: "alembic 使用"
date: 2016/08/05 10:17
tags: [alembic]
categories: Python

---

```shell
$ mkdir -p ~/Downloads/alembic_demo
$ cd ~/Downloads/alembic_demo
$ alembic init migrations
$ vi alembic.ini (修改 sqlalchemy.url = mysql://momoso:momoso@localhost/test)
$ alembic revision -m "init"
$ vi ~/Downloads/alembic_demo/migrations/versions/0011f9128b64_init.py (修改 upgrade & downgrade)
$ alembic revision -m "add desc and started at"
$ vi ~/Downloads/alembic_demo/migrations/versions/b2573182b92a_add_desc_and_started_at.py (修改)
$ alembic upgrade head
```

```
.
├── alembic.ini
└── mmigrations
    ├── README
    ├── env.py
    ├── script.py.mako
    └── versions
        ├── 0011f9128b64_init.py
        ├── 3350d7a1b145_add_groupon_table.py
        ├── 36211f69e618_add_fields_in_admin.py
        └── b2573182b92a_add_desc_and_started_at.py
```




