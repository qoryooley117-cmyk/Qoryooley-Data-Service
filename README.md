import 'package:flutter/material.dart';
import 'package:flutter_ussd/flutter_ussd.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Data Service App',
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      home: const HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  // USSD codes (tusaale ahaan)
  final String codeHormuud = "*712*611093000*0.8#";
  final String codeSomtel = "*712*611093000*0.65#";
  final String codeSomnet = "*712*611093000*0.7#";

  Future<void> sendUSSD(String code) async {
    try {
      await FlutterUssd.sendUssd(code);
    } catch (e) {
      print("Error sending USSD: $e");
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Data Service"),
        centerTitle: true,
      ),
      body: Padding(
        padding: const EdgeInsets.all(20.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () => sendUSSD(codeHormuud),
              child: const Text("Hormuud"),
            ),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: () => sendUSSD(codeSomtel),
              child: const Text("Somtel"),
            ),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: () => sendUSSD(codeSomnet),
              child: const Text("Somnet"),
            ),
          ],
        ),
      ),
    );
  }
}
