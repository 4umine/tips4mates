## 使用枚举

```java
public enum Color {

    RED(0, "红色"), GREEN(1, "绿色");

    private int code;
    private String desc;

    private Color(int code, String desc) {
        this.code = code;
        this.desc = desc;
    }

    public int getCode() {
        return this.code;
    }

    public String getDesc() {
        return this.desc;
    }
}
```

## 使用

```java
public Class Test {

    public static void main(String[] args) {
        int redCode = Color.RED.getCode();//0
        int greenCode = Color.GREEN.getCode();//1

        String redDesc = Color.RED.getDesc();//红色
        String greenDesc = Color.GREEN.getDesc();//绿色
    }
}
```