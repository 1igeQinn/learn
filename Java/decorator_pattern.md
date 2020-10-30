#装饰器模式（Decorator Pattern）
允许向现有的对象添加新功能，同时又不改变其结构。属于结构模型

```
public interface Shape{
    void draw();
} 

public class Rectangle implements Shape{
    public void draw(){
        System.out.println("Rectangle draw");
    }
}

public class Circle implements Shape{

    public void draw(){
        System.out.println("Circle shape draw");
    }
}

public abstract class ShapeDecorator implements Shape{
    protected Shape descoratedShape;

    public ShapeDecorator(Shape deShape){
        this.descoratedShape = deShape;
    }

    public void draw(){
        descoratedShape.draw();
    }
}

public RedShapeDecorator extends ShapeDecorator{

    public RedShapeDecorator(Shape shape){
        super(shape);
    }

    public void draw(){
        descoratedShape.draw();
        setRedBorder(shape);

    }

    private void setRedBorder(Shape decoratedShape){
          System.out.println("Border Color: Red");
    }

    public class Test{
        Shape circle = new Circle();
        Shape redCircle = new RedShapeDecorator(new Circle());
    }

}

```