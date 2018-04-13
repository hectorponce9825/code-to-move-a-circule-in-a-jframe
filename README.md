# code-to-move-a-circule-in-a-jframe
 //clase principal 
public class Practica_2_201700379 {

    
    //constructor
    public Practica_2_201700379 (){
        this.juego =  new Ventana(600,1000);
        this.control= new Control ();
        this.juego.addKeyListener(control);
        
        //this.juego.draw(100, 100, 80, 80);
    }
    public void jugar (){
        this.navePrincipal = new NavePrincipal(0,0,80,80); //posicion de la nave
        do{
            try{
                Thread.sleep(60);//velocidad 
            }catch(InterruptedException e){ 
            }
            this.navePrincipal.actuar(control);//la instancia de nave principal une la clase actuar y la instancia de control
            this.juego.draw(this.navePrincipal.getX(), this.navePrincipal.getY(), this.navePrincipal.getWidth(), this.navePrincipal.getHeight());//toma los valores cambiantes de las posiciones 
            //y las acciona cuando se mantiene presionado un boton de las flechas.
            
            
        }while(true);
    }
    
    
//la clase ventana
public class Ventana extends Canvas{
    
    public  Ventana(int alto, int ancho){
        JFrame Ven = new JFrame("juego");
        JPanel panel = (JPanel) Ven.getContentPane();
        super.setBounds(0, 0, ancho, alto); //super porque es la herencia
        panel.setPreferredSize(new Dimension(ancho,alto));
        panel.setLayout(null);
        
        panel.add(this);
        Ven.setBounds(150,50,ancho, alto);//dimensiones
        Ven.setVisible(true);
        Ven.addWindowListener(new WindowAdapter(){
            public void WindowClosing(WindowEvent e){
                System.exit(0); //para que al cerrar la palicacion se cierre también
            }
            
        });
        
        Ven.setResizable(false); //no se puede redireccionar la ventana
        createBufferStrategy(2);
        this.buffer = getBufferStrategy();//buffer se va a tratar de las actualizaciones del sistema 
        this.requestFocus();
        setIgnoreRepaint(true); //para que solo se actualicé cuando yo realice una accion 
        this.graphics_2D = (Graphics2D)this.buffer.getDrawGraphics(); //como se va a controlar el graphics2D con el buffer
         //anel.add(graphics_2D);
        
    }
    //método para dibujar
    public void draw (int x, int y, int ancho, int alto){
        this.graphics_2D.setColor(Color.red);
        this.graphics_2D.fillOval(x, y, alto, ancho);
        
        this.buffer.show();
    }
    //variables
    private final BufferStrategy buffer; 
    private Graphics2D graphics_2D;  //dibujar formar primitivas (opcional solo es para guiarme)
    
    
}

//la clase nave principal
public class NavePrincipal {

    public NavePrincipal(int x, int y, int width, int height) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
        this.velocidad = 10;
    }

    public void actuar (Control control){
        if(control.right){
         
            this.x += velocidad;
        }
        if(control.left){
            
            this.x -= velocidad;
        }
        if(control.up){
            
            this.y -= velocidad;    
        }
        if(control.down){
            
            this.y += velocidad; 
            
        }
    }
    
    public int getX() {
        return x;
    }

    public void setX(int x) {
        this.x = x;
    }

    public int getY() {
        return y;
    }

    public void setY(int y) {
        this.y = y;
    }

    public int getWidth() {
        return width;
    }

    public void setWidth(int width) {
        this.width = width;
    }

    public int getHeight() {
        return height;
    }

    public void setHeight(int height) {
        this.height = height;
    }
    
    private int x;
    private int y;
    private int width;
    private int height; 
    private int velocidad; 
    
}


//clase control 


public class Control implements KeyListener{

    @Override
    public void keyTyped(KeyEvent ke) {
       // throw new UnsupportedOperationException("Not supported yet."); //To change body of generated methods, choose Tools | Templates.
    }

    @Override
    public void keyPressed(KeyEvent ke) {
        switch (ke.getKeyCode()){
           /* case KeyEvent.VK_RIGHT:
                this.right = true; 
            break; 
             case KeyEvent.VK_LEFT:
                this.left = true; 
            break; */
             case KeyEvent.VK_UP:
                this.up = true; 
            break; 
             case KeyEvent.VK_DOWN:
                this.down = true; 
            break; 
            
        }
    }

    @Override
    public void keyReleased(KeyEvent ke) {
        switch (ke.getKeyCode()){
           /* case KeyEvent.VK_RIGHT:
                this.right = false; 
            break; 
             case KeyEvent.VK_LEFT:
                this.left = false; 
            break; */
             case KeyEvent.VK_UP:
                this.up = false; 
            break; 
             case KeyEvent.VK_DOWN:
                this.down = false; 
            break; 
            
        }
    }
    
    public boolean right;
    public boolean left;
    public boolean up;
    public boolean down;
    
}
    
    
    public static void main(String[] args) {
        Practica_2_201700379 game = new Practica_2_201700379();
        game.jugar();
    }
    
    
    private Ventana juego; //estancia del juego
    private Control control; //instancia de control
    private NavePrincipal navePrincipal;
    
}
