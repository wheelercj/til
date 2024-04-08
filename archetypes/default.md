+++
title = '{{ (print (strings.ToUpper (substr .File.ContentBaseName 0 1)) (substr (replace .File.ContentBaseName "-" " ") 1)) }}'
date = {{ .Date }}
+++
