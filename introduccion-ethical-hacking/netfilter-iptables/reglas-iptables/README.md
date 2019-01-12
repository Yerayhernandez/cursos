# 1. Parámetros

- **L:** Listar las reglas, se puede especificar la cadena

      ```#iptables -L [CHAIN -v][--line-numbers]```

- **A/-l i:** Agregar una regla [final o posición]

      ```#iptables -A CHAIN... // -l i CHAIN```

- **F / -D i:** Eliminar reglas[todas o la i-ésima de una cadena]

      ```#iptables -F CHAIN // -D CHAIN i

- **R i:** Reemplazar la regla i-ésima por otra nueva especificada

      ```iptables -R CHAIN i_newRule_```
