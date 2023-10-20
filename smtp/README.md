## SMTP

The **Simple Mail Transfer Protocol** (SMTP) is an Internet standard communication protocol for electronic mail transmission. Mail servers and other message transfer agents use SMTP to send and receive mail messages.
User-level [email clients](https://en.wikipedia.org/wiki/Email_client) typically use SMTP only for sending messages to a mail server for relaying, and typically submit outgoing email to the mail server on port 587 or 465 per [RFC 8314](https://datatracker.ietf.org/doc/html/rfc8314)
SMTP servers commonly use the Transmission Control Protocol on port number 25 (for plaintext) and 587 (for encrypted communications).

---

## Sequence Diagram

![SMTP Flow](https://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.githubusercontent.com/yidas/web-service-principles/main/smtp/smtp-flow.plantuml&v=20231020)

---

## References

- [Wikipedia - Simple Mail Transfer Protocol](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol)
