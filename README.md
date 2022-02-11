# 384.-StackPane-02
mesmo código anterior, mas adicionado troca de tela automatica temporizada.
INICIO
______________________
public class TesteStackPane extends StackPane {

	public TesteStackPane() {
		
		Caixa c1 = new Caixa().comTexto("Tela 1");
		Caixa c2 = new Caixa().comTexto("Tela 2");
		Caixa c3 = new Caixa().comTexto("Tela 3");
		Caixa c4 = new Caixa().comTexto("Tela 4");
		Caixa c5 = new Caixa().comTexto("Tela 5");
		Caixa c6 = new Caixa().comTexto("Tela 6");
		
		getChildren().addAll(c2, c3, c4, c5, c6, c1); // c1 colocado por utimo para que seja o primeiro
		
		setOnMouseClicked(e -> {
			if(e.getSceneX() > getScene().getWidth() / 2) {
			   getChildren().get(0).toFront();
			} else {
				getChildren().get(5).toBack();
			}
		});	
		Thread t = new Thread(() -> {
			while(true) {
				try {
					Thread.sleep(2000); // dorme por 3 segundos
					
					Platform.runLater(() -> { //Inserir Platform pois aparece msg de erro de not on FX app 
						getChildren().get(0).toFront();
					});
				} catch (Exception e) {
					System.out.println(e.getMessage());
				}
			}
		});
		t.setDaemon(true);// Garante que se a Thread principal fechar as demais tbm vao fechar
		t.start();
	}
}
