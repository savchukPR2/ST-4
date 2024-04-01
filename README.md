# ST-4 UNIT-тестирование с использованием MSTest в среде .NET


![GitHub pull requests](https://img.shields.io/github/issues-pr/UNN-CS/ST-4)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/UNN-CS/ST-4)

Срок выполнения задания:

**по 07.04.24** ![Relative date](https://img.shields.io/date/1712523600)


## Задание
```csharp
using Stateless;

public class Bug {
   public enum State {Open, Assigned, Defered, Closed}
   private enum Trigger {Assign, Defer, Close}
   private StateMachine<State, Trigger> sm;

   public Bug(State state) {
      sm = new StateMachine<State, Trigger>(state);
      sm.Configure(State.Open)
            .Permit(Trigger.Assign, State.Assigned);
      sm.Configure(State.Assigned)
            .Permit(Trigger.Close, State.Closed)
            .Permit(Trigger.Defer, State.Defered)
            .Ignore(Trigger.Assign);
      sm.Configure(State.Closed)
            .Permit(Trigger.Assign, State.Assigned);
      sm.Configure(State.Defered)
            .Permit(Trigger.Assign, State.Assigned); 
   }
   public void Close() {
      sm.Fire(Trigger.Close);
      Console.WriteLine("Close");
   }
   public void Assign() {
      sm.Fire(Trigger.Assign);
      Console.WriteLine("Assign");   
   }
   public void Defer() {
      sm.Fire(Trigger.Defer);
      Console.WriteLine("Defer");   
   }   
   public State getState() {
      return sm.State;
   }
}

public class Program {
   public static void Main(string[] args) {
      var bug = new Bug(Bug.State.Open);
      bug.Assign();
      bug.Close();
      bug.Assign();
      bug.Defer();
      bug.Assign();
      Console.WriteLine(bug.getState());
   }
}
```
