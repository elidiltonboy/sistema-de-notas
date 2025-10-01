from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer
from reportlab.lib.styles import getSampleStyleSheet

# Função para cadastrar notas
def cadastrar_notas():
    notas = []
    while True:
        try:
            nota = float(input("Digite uma nota (ou -1 para finalizar): "))
            if nota == -1:
                break
            if 0 <= nota <= 10:
                notas.append(nota)
            else:
                print("⚠️ Nota inválida! Digite entre 0 e 10.")
        except ValueError:
            print("⚠️ Entrada inválida! Digite um número.")
    return notas

# Função para calcular média
def calcular_media(notas):
    if len(notas) == 0:
        return 0
    return sum(notas) / len(notas)

# Função para verificar situação
def verificar_situacao(media):
    return "APROVADO ✅" if media >= 7 else "REPROVADO ❌"

# Função para gerar PDF
def gerar_relatorio_pdf(notas, media, situacao, nome_arquivo="relatorio.pdf"):
    doc = SimpleDocTemplate(nome_arquivo, pagesize=A4)
    estilos = getSampleStyleSheet()
    elementos = []

    elementos.append(Paragraph("<b>RELATÓRIO FINAL</b>", estilos['Title']))
    elementos.append(Spacer(1, 20))
    elementos.append(Paragraph(f"Notas inseridas: {notas}", estilos['Normal']))
    elementos.append(Paragraph(f"Média: {media:.2f}", estilos['Normal']))
    elementos.append(Paragraph(f"Situação: {situacao}", estilos['Normal']))

    doc.build(elementos)
    print(f"📄 Relatório gerado: {nome_arquivo}")

# Programa principal
def main():
    print("=== SISTEMA DE GESTÃO DE NOTAS ===")
    notas = cadastrar_notas()
    media = calcular_media(notas)
    status = verificar_situacao(media)
    gerar_relatorio_pdf(notas, media, status)

# Executar
main()
