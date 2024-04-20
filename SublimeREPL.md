# SublimeREPL
Accede a la documentación de la herramienta en
[click here](https://sublimerepl.readthedocs.io/en/latest/)

# To open a repl:
- ctrl + shift + p
- escribir: repl lisp

# Como evaluar una linea en el repl
ctrl + ,, soltar l

# Como enviar una linea al repl
ctrl + shift + ,, (soltar todas las teclas) presionar: (L minuscula) l
control mas shift comma comma, solar y presionar L


# Key binding
editar la configuración de sublime y agregar esta config.
servira para enviar el archivo fuente a lisp presiando: alt+ctrl+h

[
	{
	  "keys": ["alt+ctrl+h"],
	  "command": "repl_open",
	  "args": {
	   	"type": "subprocess",
	   	"encoding": "utf8",
	   	"cmd": ["/usr/bin/clisp", "-repl", "$file"],
	   	"cwd": "$file_path",
	   	"external_id": "lisp",
	   	"syntax": "Packages/Lisp/Lisp.tmLanguage"
  	}
  }
]
