runs-on: ubuntu-latest

steps:
- name: 📥 Checkout
  uses: actions/checkout@v4
  
- name: 🔧 Setup .NET
  uses: actions/setup-dotnet@v4
  with:
    dotnet-version: '8.0.x'
    
- name: 📦 Restore
  run: dotnet restore
  
- name: 🔨 Build
  run: dotnet build --no-restore --configuration Release
  
- name: 🧪 Test
  run: dotnet test --no-build --configuration Release --verbosity normal
  
- name: 📊 Upload coverage
  if: success()
  uses: codecov/codecov-action@v3

