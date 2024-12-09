Detalhes das Funcionalidades

Pacote PKG_ALUNO

- Procedure de Exclusão de Aluno
Recebe um parâmetro P_ID_ALUNO do tipo NUMBER.
Exclui todas as entradas da tabela MATRICULA associadas ao aluno antes de excluir o próprio registro na tabela ALUNO.
Usa transações explícitas (COMMIT e ROLLBACK) para garantir a consistência.
- Cursor de Listagem de Alunos Maiores de 18 Anos
Calcula a idade usando a função MONTHS_BETWEEN dividida por 12 para determinar os anos.
Seleciona o nome e a data de nascimento dos alunos que têm mais de 18 anos.
- Cursor Parametrizado com Filtro por Curso
Recebe um parâmetro P_ID_CURSO para filtrar os alunos matriculados no curso.
Realiza um JOIN entre as tabelas ALUNO e MATRICULA para retornar os nomes dos alunos.



Pacote PKG_PROFESSOR

- Cursor para Total de Turmas por Professor
Consulta: Retorna os nomes dos professores e o total de turmas para cada um.
Filtro: Apenas os professores responsáveis por mais de uma turma (HAVING COUNT(T.ID_TURMA) > 1).
Relaciona as tabelas PROFESSOR e TURMA.
- Function TOTAL_TURMAS
Entrada: Recebe o ID do professor (P_ID_PROFESSOR).
Saída: Retorna o número de turmas associadas ao professor na tabela TURMA.
Utiliza a função COUNT em uma consulta direta.
Lida com exceções para garantir que, caso o professor não tenha turmas, o retorno seja 0.
- Function PROFESSOR_DISCIPLINA
Entrada: Recebe o ID da disciplina (P_ID_DISCIPLINA).
Saída: Retorna o nome do professor associado à disciplina.
Relaciona as tabelas PROFESSOR e DISCIPLINA utilizando o campo ID_PROFESSOR.
Lida com exceções para casos em que não há professor associado à disciplina.


Pacote PKG_DISCIPLINA

- Procedure CADASTRAR_DISCIPLINA
Entrada: Recebe P_NOME, P_DESCRICAO e P_CARGA_HORARIA como parâmetros.
Saída: Insere os dados na tabela DISCIPLINA.
Usa transações explícitas (COMMIT e ROLLBACK) para garantir consistência.
- Cursor TOTAL_ALUNOS_POR_DISCIPLINA
Consulta: Retorna as disciplinas com mais de 10 alunos matriculados, exibindo o nome da disciplina e o total de alunos.
Relaciona as tabelas DISCIPLINA e MATRICULA.
- Cursor MEDIA_IDADE_DISCIPLINA
Parâmetro: Recebe P_ID_DISCIPLINA como filtro.
Consulta: Calcula a média de idade dos alunos matriculados na disciplina, considerando a diferença em anos entre a data de nascimento e a data atual.
- Procedure LISTAR_ALUNOS_DISCIPLINA
Entrada: Recebe o ID da disciplina (P_ID_DISCIPLINA).
Saída: Exibe os nomes dos alunos matriculados na disciplina usando DBMS_OUTPUT.PUT_LINE.