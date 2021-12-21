## Live Templates Bloc

`Generate Bloc ver.>8 with freezed`
```dart
import 'package:bloc/bloc.dart';
import 'package:freezed_annotation/freezed_annotation.dart';

part '$fileName$.freezed.dart';

@freezed
class $NAME$Event with _$$$NAME$Event {
  const $NAME$Event._();

  const factory $NAME$Event.load() = Load$NAME$Event;

  const factory $NAME$Event.change() = Change$NAME$Event;

  const factory $NAME$Event.save() = Save$NAME$Event;

}

@freezed
class $NAME$State with _$$$NAME$State {
  const $NAME$State._();
  
  const factory $NAME$State.initial() = Initial$NAME$State;
  
  const factory $NAME$State.loading() = Loading$NAME$State;
  
  const factory $NAME$State.loaded() = Loaded$NAME$State;
  
  const factory $NAME$State.error() = Error$NAME$State;
  
  const factory $NAME$State.idle() = Idle$NAME$State;
}

class $NAME$Bloc extends Bloc<$NAME$Event, $NAME$State> {
  $NAME$Bloc() : super(const Initial$NAME$State()) {
    on<Load$NAME$Event>(_onLoad$NAME$Event);
    on<Change$NAME$Event>(_onChange$NAME$Event);
    on<Save$NAME$Event>(_onSave$NAME$Event);
  }$END$
  
  Future<void> _onLoad$NAME$Event(
    Load$NAME$Event event,
    Emitter<$NAME$State> emit,
  ) async {
    emit(const $NAME$State.loading());
    // ... code
  }

  Future<void> _onChange$NAME$Event(
    Change$NAME$Event event,
    Emitter<$NAME$State> emit,
  ) async {
    // emit();
  }

  Future<void> _onSave$NAME$Event(
    Save$NAME$Event event,
    Emitter<$NAME$State> emit,
  ) async {
    // emit();
  }
}
```

`Generate Bloc Ver.<8 with freezed`
```dart
import 'package:bloc/bloc.dart';
import 'package:freezed_annotation/freezed_annotation.dart';

part '$fileName$.freezed.dart';

@freezed
abstract class $NAME$Event with _$$$NAME$Event {
  const $NAME$Event._();

  const factory $NAME$Event.load() = Load$NAME$Event;

  const factory $NAME$Event.change() = Change$NAME$Event;

  const factory $NAME$Event.save() = Save$NAME$Event;

}

@freezed
abstract class $NAME$State with _$$$NAME$State {
  const $NAME$State._();
  
  const factory $NAME$State.initial() = Initial$NAME$State;
  
  const factory $NAME$State.loading() = Loading$NAME$State;
  
  const factory $NAME$State.loaded() = Loaded$NAME$State;
}

class $NAME$BLoC extends Bloc<$NAME$Event, $NAME$State> {
  $NAME$BLoC() : super(const Initial$NAME$State());

  @override
  Stream<$NAME$State> mapEventToState($NAME$Event event) =>
    event.when<Stream<$NAME$State>>(
      load: _load,
      change: _change,
      save: _save,
    );$END$
  
  Stream<$NAME$State> _load() async* {
    // ...code    
  }

  Stream<$NAME$State> _change() async* {
    // ...code
  }

  Stream<$NAME$State> _save() async* {
    // ...code
  }
}
```

`Create BlocObserver with Crashlytics`
```dart
class _MainBlocObserver extends BlocObserver {
/* INIT Bloc.observer
if (kDebugMode) {
  Bloc.observer = _MainBlocObserver();
}
*/
  @override
  Future<void> onError(BlocBase bloc, Object error, StackTrace stackTrace) async {
    super.onError(bloc, error, stackTrace);
    await FirebaseCrashlytics.instance
        .recordError(error, stackTrace, reason: 'Crash in bloc: ${bloc.runtimeType} , state: ${bloc.state}');
  }
}
```

`Create BlocObserver with Crashlytics`
```dart
class _MainBlocObserver extends BlocObserver {
/* INIT Bloc.observer
if (kDebugMode) {
  Bloc.observer = _MainBlocObserver();
}
*/
  @override
  Future<void> onError(BlocBase bloc, Object error, StackTrace stackTrace) async {
    super.onError(bloc, error, stackTrace);
    await FirebaseCrashlytics.instance
        .recordError(error, stackTrace, reason: 'Crash in bloc: ${bloc.runtimeType} , state: ${bloc.state}');
  }
}
```

## Live Templates Freezed

`Generate Freezed class`
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part '$fileName$.freezed.dart';

@freezed
class $NAME$ with _$$$NAME$ {
  const factory $NAME$({
       @Default(1) int? id,
      $END$
  }) = _$NAME$;
}
```

`Generate Freezed class with json`
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part '$fileName$.freezed.dart';
part '$fileName$.g.dart';

@freezed
class $NAME$ with _$$$NAME$ {
  const factory $NAME$({
    @JsonKey(name: 'id')
    @Default(1) int? id,
    $END$
  }) = _$NAME$;

  factory $NAME$.fromJson(Map<String, dynamic> json) => _$$$NAME$FromJson(json);
}
```

## Live Templates Inherited widget

`Create Inherited widget`
```dart
class $NAME$ extends InheritedWidget {
  const $NAME$({
    Key? key,
    required Widget child,
  }) : super(key: key, child: child);

  static $NAME$ of(BuildContext context) {
    final $NAME$? result = context.dependOnInheritedWidgetOfExactType<$NAME$>();
    assert(result != null, 'No $NAME$ found in context');
    return result!;
  }

  @override
  bool updateShouldNotify($NAME$ oldWidget) {
    return true;
  }
}
```


## Live Templates Inherited widget

`Create Inherited widget`
```dart
class $NAME$ extends InheritedWidget {
  const $NAME$({
    Key? key,
    required Widget child,
  }) : super(key: key, child: child);

  static $NAME$ of(BuildContext context) {
    final $NAME$? result = context.dependOnInheritedWidgetOfExactType<$NAME$>();
    assert(result != null, 'No $NAME$ found in context');
    return result!;
  }

  @override
  bool updateShouldNotify($NAME$ oldWidget) {
    return true;
  }
}
```

## Live Templates Stream Tranformer

`Create Stream Tranformer`
```dart
class $NAME$StreamTransformer<$FROM$, $TO$> extends StreamTransformerBase<$FROM$, $TO$> {

  const $NAME$StreamTransformer();

  @override
  Stream<$TO$> bind(Stream<$FROM$> stream) {
    StreamSubscription<$FROM$> sub;
    final sc = StreamController<$TO$>(
        onPause: () => sub.pause(),
        onResume: () => sub.resume(),
        onCancel: () => sub.cancel(),
        sync: true,
      ) as SynchronousStreamController<$TO$>;
    sub = stream.listen((value) {
        $END$
        sc.add(value as $TO$);
      },
      onDone: sc.close,
      onError: sc.addError,
      cancelOnError: true,
    );
    return stream.isBroadcast
      ? sc.stream.asBroadcastStream()
      : sc.stream;
  }
}

extension $NAME$Extensions<$FROM$> on Stream<$FROM$> {
  Stream<$TO$> $decapitalizeNAME$<$TO$>() =>
    transform<$TO$>($NAME$StreamTransformer<$FROM$, $TO$>());
}
```
