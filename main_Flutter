import 'package:flutter/material.dart';
import 'dart:async';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(title: 'Flutter Demo', home: const TimerScreen());
  }
}

class TimerScreen extends StatefulWidget {
  const TimerScreen({super.key});

  @override
  State<TimerScreen> createState() => _TimerScreenState();
}

class _TimerScreenState extends State<TimerScreen> {
  int _timeInSeconds = 0;
  bool _isRunning = false;
  late Timer _timer;

  void _startTimer() {
    if (_isRunning) return;
    _isRunning = true;
    _timer = Timer.periodic(const Duration(seconds: 1), (timer) {
      if (_timeInSeconds > 0) {
        setState(() {
          _timeInSeconds--;
        });
      } else {
        _timer.cancel();
        setState(() {
          _isRunning = false;
        });
      }
    });
  }

  void _stopTimer() {
    _timer.cancel();
    setState(() {
      _isRunning = false;
    });
  }

  void _resetTimer() {
    _timer.cancel();
    setState(() {
      _timeInSeconds = 0;
      _isRunning = false;
    });
  }

  Future<void> _setTimer() async {
    int? newTime = await showDialog<int>(
      context: context,
      builder: (context) {
        int tempTime = 0;
        return AlertDialog(
          title: const Text('Set Timer'),
          content: TextField(
            keyboardType: TextInputType.number,
            onChanged: (value) {
              tempTime = int.tryParse(value) ?? 0;
            },
            decoration: const InputDecoration(labelText: 'Seconds'),
          ),
          actions: [
            TextButton(
              onPressed: () => Navigator.of(context).pop(tempTime),
              child: const Text('Set'),
            ),
          ],
        );
      },
    );
    if (newTime != null) {
      setState(() {
        _timeInSeconds = newTime;
      });
    }
  }

  String _formatTime(int seconds) {
    int minutes = seconds ~/ 60;
    int remainingSeconds = seconds % 60;
    return '${minutes.toString().padLeft(2, '0')}:${remainingSeconds.toString().padLeft(2, '0')}';
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Timer App'),
        backgroundColor: Colors.white,
        elevation: 0.0,
        centerTitle: true,
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              _formatTime(_timeInSeconds),
              style: const TextStyle(fontSize: 50, fontWeight: FontWeight.bold),
            ),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: _setTimer,
              child: const Text('Set Timer'),
            ),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: _isRunning ? _stopTimer : _startTimer,
              child: Text(_isRunning ? 'Stop' : 'Start'),
            ),
            const SizedBox(height: 20),
            ElevatedButton(onPressed: _resetTimer, child: const Text('Reset')),
          ],
        ),
      ),
    );
  }
}
