---
title:  changed_when - idempotency
categories:
- ansible 
author: Oliver Gaida
version: 1
---

Question: How to ensure idempotency in ansible tasks with shell module?

What is idempotency?

Idempotency is the property of an operation in computer science and mathematics where an action can be performed multiple times without changing the result beyond the initial application. It ensures that repeating a request (e.g., retrying a failed API call) produces the same system state as a single request, preventing duplicate data or unintended side effects

Sample-Solution:

```yaml
---
- hosts: localhost
  name: changed_when test
  gather_facts: no
  tasks:
    - name: create file /tmp/test42
      shell: |
        if [ -e /tmp/test42 ]
        then
          echo ok
        else 
          touch /tmp/test42
          echo changed
        fi
      args:
        executable: bash
      register: result
      changed_when: '"changed" in result.stdout'
```

{% include youtube.html id="DBfirX9o2KI" %}
