import java.util.ArrayList;
import java.util.List;

// Classe base para todos os eventos
abstract class Evento {
    protected String nome;
    protected String data;
    protected String local;

    public Evento(String nome, String data, String local) {
        this.nome = nome;
        this.data = data;
        this.local = local;
    }

    // Método abstrato que deve ser implementado pelas subclasses
    public abstract void agendarEvento();
}

// Classe Reuniao, derivada de Evento
class Reuniao extends Evento {
    private boolean isPrivada;
    private String senhaAcesso;

    public Reuniao(String nome, String data, String local, boolean isPrivada, String senhaAcesso) {
        super(nome, data, local);
        this.isPrivada = isPrivada;
        this.senhaAcesso = senhaAcesso;
    }

    @Override
    public void agendarEvento() {
        System.out.println("Reunião '" + nome + "' agendada para " + data + " em " + local);
        if (isPrivada) {
            System.out.println("Esta reunião é privada. Senha de acesso: " + senhaAcesso);
        } else {
            System.out.println("Esta reunião é pública.");
        }
    }
}

// Classe Evento Corporativo, derivada de Evento
class EventoCorporativo extends Evento {
    private List<String> ambientesReservados;

    public EventoCorporativo(String nome, String data, String local, List<String> ambientesReservados) {
        super(nome, data, local);
        this.ambientesReservados = ambientesReservados;
    }

    // Verifica se os ambientes estão disponíveis (simulação)
    private boolean verificarAmbientes() {
        // Simulação: todos os ambientes estão disponíveis
        return true;
    }

    @Override
    public void agendarEvento() {
        if (verificarAmbientes()) {
            System.out.println("Evento Corporativo '" + nome + "' agendado para " + data + " em " + local);
            System.out.println("Ambientes reservados: " + ambientesReservados);
        } else {
            System.out.println("Falha ao agendar o evento corporativo. Ambientes não disponíveis.");
        }
    }
}

// Classe Workshop, derivada de Evento
class Workshop extends Evento {
    private int maxParticipantes;
    private int participantesInscritos;

    public Workshop(String nome, String data, String local, int maxParticipantes) {
        super(nome, data, local);
        this.maxParticipantes = maxParticipantes;
        this.participantesInscritos = 0;
    }

    // Método para inscrever participantes, verificando o limite
    public void inscreverParticipante() {
        if (participantesInscritos < maxParticipantes) {
            participantesInscritos++;
            System.out.println("Participante inscrito com sucesso. Total de inscritos: " + participantesInscritos);
        } else {
            System.out.println("Limite de participantes atingido. Não é possível inscrever mais.");
        }
    }

    @Override
    public void agendarEvento() {
        System.out.println("Workshop '" + nome + "' agendado para " + data + " em " + local);
        System.out.println("Limite de participantes: " + maxParticipantes);
    }
}

// Classe principal para execução do sistema
public class SistemaAgendamento {
    public static void main(String[] args) {
        // Agendar uma reunião privada
        Reuniao reuniaoPrivada = new Reuniao("Reunião de Estratégia", "10/10/2024", "Sala 101", true, "1234");
        reuniaoPrivada.agendarEvento();

        // Agendar um evento corporativo
        List<String> ambientes = new ArrayList<>();
        ambientes.add("Sala de Conferência");
        ambientes.add("Área de Refeições");
        EventoCorporativo eventoCorporativo = new EventoCorporativo("Conferência Anual", "20/11/2024", "Hotel Lux", ambientes);
        eventoCorporativo.agendarEvento();

        // Agendar um workshop e inscrever participantes
        Workshop workshop = new Workshop("Workshop de Java", "15/09/2024", "Sala 202", 2);
        workshop.agendarEvento();
        workshop.inscreverParticipante();
        workshop.inscreverParticipante();
        workshop.inscreverParticipante(); // Excede o limite
    }
}
