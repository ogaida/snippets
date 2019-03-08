# negation


```yaml
- shell: echo "This certainly isn't epic!"
  when: not epic
```

# Variable gesetzt?


```yaml
- shell: echo "I've got '{{ foo }}' and am not afraid to use it!"
  when: foo is defined

- fail: msg="Bailing out. this play requires 'bar'"
  when: bar is undefined
```

# Substring ist enthalten

```yaml
- shell: echo "motd contains the word hi"
  when: motd_contents.stdout.find('hi') != -1
```

[Home](./)
