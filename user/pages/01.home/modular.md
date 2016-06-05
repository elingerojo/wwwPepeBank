---
title: Home
menu: Home
form:
    name: my-nice-form
    action: /home
    fields:
        - name: name
          id: name
          label: Name
          classes: form-control form-control-lg
          placeholder: Teclee su nombre
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          id: email
          classes: form-control form-control-lg
          label: Email
          placeholder: Teclee su eMail
          type: text
          validate:
            rule: email
            required: true

        - name: message
          label: Message
          classes: form-control form-control-lg
          size: long
          placeholder: Teclee su mensaje
          type: textarea
          validate:
            required: true

    buttons:
        - type: submit
          value: Enviar Mensaje
          class: btn btn-primary btn-block

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.from }}"
              - "{{ form.value.email }}"
            subject: "[Feedback] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Thank you for your feedback!
        - display: thankyou


onpage_menu: true
content:
    items: @self.modular
    order:
        by: default
        dir: asc
        custom:
            - _intro
            - _features
            - _video
            - _pricing
            - _testimonials
            - _text
            - _news
            - _contact
---
