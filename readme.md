# :runner: runcs

Runs a C# file using .NET 10+

## Usage

```
- name: 🏃‍♂️ C#
  uses: devlooped/actions-runcs@v1
  id: runcs
  with:
    # If args has newlines, it will be properly quoted/escaped
    args: |
      --message
      Hi "kzu", I can even mix 'single' quotes
    # Script can be an inline C# script, including nuget packages
    script: |
      #:package Humanizer@2.*
      using Humanizer;
  
      var date = DateTime.Parse("${{ github.event.inputs.date }}");
      var elapsed = DateTime.Now - date;
  
      if (elapsed.TotalSeconds > 0)
          Console.WriteLine($"It's been {elapsed.Humanize()} since {date.Humanize()}");
      else
          Console.WriteLine($"Still {elapsed.Negate().Humanize()} until {date.Humanize()}");
```

You can also specify a file to run:

```
- name: 🏃‍♂️ C#
  uses: ./.github/actions/runcs
  with:
    file: ./script.cs
```

