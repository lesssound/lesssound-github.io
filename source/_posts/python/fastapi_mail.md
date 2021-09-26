title: fastapi send mail
categories:
  - python
date: 2021-08-17 17:40:50
---
```sh

from fastapi import FastAPI, BackgroundTasks, UploadFile, File, Form
from starlette.responses import JSONResponse
#  from starlette.requests import Request
from fastapi_mail import FastMail, MessageSchema, ConnectionConfig
from pydantic import BaseModel, EmailStr
from typing import List, Text


class EmailSchema(BaseModel):
    email: List[EmailStr]
    html: Text

conf = ConnectionConfig(
	# update username, password, from
    MAIL_USERNAME="123456",
    MAIL_PASSWORD="password",
    MAIL_FROM="123456@qq.com",
    
    MAIL_PORT=587,
    MAIL_SERVER="smtp.qq.com",
    MAIL_TLS=True,
    MAIL_SSL=False,
    USE_CREDENTIALS=True,
    VALIDATE_CERTS=True,
)

app = FastAPI()


html = """
<p>Thanks for using Fastapi-mail</p>
"""


@app.post("/email")
async def simple_send(email: EmailSchema) -> JSONResponse:

    message = MessageSchema(
        subject="Fastapi-Mail module",
        recipients=email.dict().get(
            "email"
        ),  # List of recipients, as many as you can pass
        body=email.dict().get("html", html),
        subtype="html",
    )

    fm = FastMail(conf)
    await fm.send_message(message)
    return JSONResponse(status_code=200, content={"message": "email has been sent"})


@app.post("/file")
async def send_file(
    background_tasks: BackgroundTasks,
    file: UploadFile = File(...),
    email: EmailStr = Form(...),
) -> JSONResponse:

    message = MessageSchema(
        subject="Fastapi mail module",
        recipients=[email],
        body="Simple background task ",
        attachments=[file],
    )

    fm = FastMail(conf)

    background_tasks.add_task(fm.send_message, message)

    return JSONResponse(status_code=200, content={"message": "email has been sent"})

if __name__ == '__main__':
    uvicorn.run('main:app', reload=True)
```