---
title: settings
categories:
  - python
date: 2021-07-17 11:34:39
tags:
  - python
---


{% codeblock "code" lang:python %}
import os
import sys

import yaml
from loguru import logger
from dotenv import load_dotenv

BASE_DIR = os.path.abspath(os.path.dirname(__file__)).rstrip("/common")

log_file_path = os.path.join(BASE_DIR, "logs/stdout.log")
err_log_file_path = os.path.join(BASE_DIR, "logs/error.log")

logger.add(
    log_file_path,
    format="{process} {thread} {time:YYYY.MM.DD HH.mm.ss} {level}.{file}.{name}.{module}.{line} {message}",
    rotation="100 MB",
    colorize=True,
    enqueue=True,
    backtrace=True,
    diagnose=True,
    level="INFO",
)
logger.add(
    err_log_file_path,
    format="{time:YYYY.MM.DD HH.mm.ss} {level}.{file}.{name}.{module}.{line} {message}",
    rotation="100 MB",
    level="ERROR",
    colorize=True,
    enqueue=True,
    backtrace=True,
    diagnose=True,
)


class ConfigMeta:
    def __init__(self, _file="config.yaml"):
        self.file = _file

    def __getattr__(self, key):
        with open(self.file, "r") as file:
            self.con = yaml.safe_load(file)
        result = self.con.get(key)
        if not result:
            load_dotenv()
            result = os.getenv(key)
        return result


Config = ConfigMeta()

{% endcodeblock %}
