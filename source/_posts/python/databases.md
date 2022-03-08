title: databases
categories:
  - python
tags:
  - sqlalchemy
date: 2021-07-17 11:31:42
---
### sqlalchemy

{% codeblock "安装及导出model" lang:sh %}
# pip install psycopg2-binary
# sqlacodegen postgres://user:passwd@host:ip/database --outfile model.py
{% endcodeblock %}


{% codeblock "code" lang:sh >folded %}

from sqlalchemy import create_engine
from sqlalchemy import Column, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

db_string = "postgres://admin:donotusethispassword@aws-us-east-1-portal.19.dblayer.com:15813/compose"

db = create_engine(db_string)
base = declarative_base()


class Film(base):
    __tablename__ = "films"

    title = Column(String, primary_key=True)
    director = Column(String)
    year = Column(String)


Session = sessionmaker(db)
session = Session()

base.metadata.create_all(db)

# Create
doctor_strange = Film(title="Doctor Strange", director="Scott Derrickson", year="2016")
session.add(doctor_strange)
session.commit()

# Read
films = session.query(Film)
for film in films:
    print(film.title)

# Update
doctor_strange.title = "Some2016Film"
session.commit()

# Delete
session.delete(doctor_strange)
session.commit()

delete_obj = Shop.__table__.delete().where(Shop.shop_cate.contains("m"))
session.execute(delete_obj)
session.commit()
{% endcodeblock %}

{% codeblock "databases" lang:sh %}
# pip install 'databases[aiomysql]' aiomysq
import asyncio

# Create a database instance, and connect to it.
from databases import Database


async def run():
    db_url = "mysql://user:passwd@host:port/db"
    database = Database(db_url)
    #  database = Database("sqlite+aiosqlite:///example.db")
    await database.connect()

    # Create a table.
    #  query = """CREATE TABLE HighScores (id INTEGER PRIMARY KEY AUTO_INCREMENT, name VARCHAR(100), score INTEGER)"""
    #  await database.execute(query=query)

    # Insert some data.
    query = "INSERT INTO HighScores(name, score) VALUES (:name, :score)"
    values = [
        {"name": "Daisy", "score": 92},
        {"name": "Neil", "score": 87},
        {"name": "Carol", "score": 43},
    ]
    await database.execute_many(query=query, values=values)

    # Run a database query.
    query = "SELECT * FROM HighScores"
    rows = await database.fetch_all(query=query)
    print("High Scores:", rows)
    for r in rows:
        print(r)
    return rows


loop = asyncio.get_event_loop()
loop.run_until_complete(run())

{% endcodeblock %}