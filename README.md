1 - Considere o seguinte arquivo de entrada com a lista dos dez nomes mais comuns no Brasil para Meninos  e  Meninas. Pede-se  que  o  arquivo  seja  separado em dois,  um apenas para  meninos e outro para meninas.

Ranking Meninos       Ranking Meninas

1 Miguel              1 Sophia
2 Davi                2 Alice
3 Arthur              3 Julia
4 Pedro               4 Isabella
5 Gabriel             5 Manuela
6 Bernardo            6 Laura
7 Lucas               7 Luiza
8 Matheus Luz         8 Valentina
9 Rafael              9 Giovanna
10 Heitor             10 Maria Eduarda

    R=
      > 1.sh
      chmod +x 1.sh
      vim 1.sh
        
        #!/bin/bash
	
	sed -E 's/ /./g' < lista.txt > listajunta
	awk '{print $1}' < listajunta > lista_meninos
	tr '.' ' ' < lista_meninos > lista_oficial
	
	awk '{print $2}' < listajunta > lista_meninas
	tr '.' ' ' < lista_meninas > lista_meninas_oficial
	
	cat lista_oficial
	echo "-----------------------"
	cat lista_meninas_oficial

2 - Dado  um  arquivo  com  a lista de todos  os  downloads efetuados  pelos  usuários  no  último  mês,  deseja-se totalizar quanto cada usuário baixou. Segue o formato do arquivo:

Nelson www.google.com.br 250
Arr445 www.testes.com/dbz.wmv 20050
Nelson www.uol.com.br 300
Vianna debian.org/9.7.0.iso 800555

3 - Escreva um script que exiba um menu que, usando o sed:

r - Digite o nome de um arquivo que será processado.
a - Remova todas as letras do arquivo.
b - Remova todos os dígitos do arquivo.
c - Substitua todos os caracteres que não são letras nem dígitos do arquivo por ~.
q - Saia do script.

4 - Escreva um script que remova todos os endereços IP de um arquivo de entrada, alterando o seu valor para **!!CENSU--RADO!!**.



5 - Escreva um script que, dado uma lista de números de telefone no formato xxxxxxxxxxx, coloque cada telefone no formato (xx) x xxxx-xxxx. Exemplo:

Para o seguinte arquivo:

	12345678900 Alberto
	11111111111 Augusto
	83987654321 Almirante
A saída deve ser:

	(12) 3 4567-8900 Alberto
	(11) 1 1111-1111 Augusto
	(83) 9 8765-4321 Almirante

Use a criatividade para os nomes de contatos na sua lista de números.

    R=
      > num
      vim num 
      	12345678900 Thor
	      11111111111 Galalau
	      83987654321 Papaleguas
      > 5.sh
      chmod +x 5.sh
      vim 5.sh
        
        #!/bin/bash
        
        a=$1
        
        $(awk '{print $1}' < $a > num.txt)
        $(awk '{print $2}' < $a > nome.txt)
        
        arq=$(cat nome.txt)
        
        sed 's/\(..\)\(.\{1\}\)\(.\{4\}\)/(\1) \2 \3-/g' < num.txt > lista_num.txt
        
        cont=0
        
        for i in $arq; do
            cont=$(( cont + 1 ))
            sed "s/$/ $i/" < lista_num.txt >> $i.txt
            cat $i.txt | head -n$cont | tail -n 1 >> nova_lista
            rm $i.txt
         done
         
         cat nova_lista
         rm nova_lista
