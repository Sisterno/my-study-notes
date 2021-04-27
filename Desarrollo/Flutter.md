# Flutter

### Por que?

Mis padres trabajan en la distribucion de mercaderia. Un dia me dijeron que su supervisor les pidio que empezaran a hacer un reporte de invetariado cada cierto tiempo y se lo pasen en excel. Para esta les dije que se los voy a hacer una app que le permita hacer el inventariado , guardarlo y luego exportarlo en excel para que lo envien facil. Y por eso me puse a trabajar con flutter. Ya tengo experiencia con java, en la U hice alguna apps con java, pero siempre odie xml(junto con soap, te odio SOAP >:v) y ahora quiero intentarlo con Flutter.

## Conceptos de Flutter

Flutter esta inspirado en el desarrollo de app webs. Mas en concreto en React. Por esta raon tenemos conceptos muy parecidoes entre estos.



### InheritedWidget - contexto

InheritedWidget es igual que el contexto de react. Los widgets de un arbol pueden haceder a la informacion de un InheritedWidget para poder leer y modificar sus datos. Todos los widgets del arbol para abajo pueden tener acceso a este 'contexto'.

```dart
class InheritedDataProvider extends InheritedWidget {
    final Data data;
    InheritedDataProvider({
        Widget child,
        this.data,
    }) : super(child: child);
    @override
    bool updateShouldNotify(InheritedDataProvider oldWidget) => data != oldWidget.data;
    static InheritedDataProvider of(BuildContext context) => context.inheritFromWidgetOfExactType(InheritedDataProvider);
}
```
