# Network-Latency-Optimization-Utility
// LatencyTester.go

package main

import (
	"fmt"
	"time"
)

// Define the assumed address of the game server
const gameServerAddress = "game.competitivebattle.net:8080"
const testAttempts = 5

// Simulate a network request and measure RTT latency
func measureLatency(address string) (time.Duration, error) {
    // In a real application, this would involve a connection handshake (e.g., TCP)
    // Here, we simulate a variable network delay.
    
    start := time.Now()
    
    // Simulate network delay based on a rough average
    // In a real scenario, this would involve actual I/O
    simulatedDelay := time.Duration(10 + (time.Now().UnixNano() % 50)) * time.Millisecond 
    time.Sleep(simulatedDelay)
    
    rtt := time.Since(start)
    return rtt, nil
}

func main() {
    fmt.Printf("Testing latency to: %s\n", gameServerAddress)
    
    var totalLatency time.Duration
    
    for i := 0; i < testAttempts; i++ {
        latency, err := measureLatency(gameServerAddress)
        if err != nil {
            fmt.Printf("Attempt %d failed: %v\n", i+1, err)
            continue
        }
        fmt.Printf("Attempt %d RTT: %v\n", i+1, latency)
        totalLatency += latency
    }
    
    averageLatency := totalLatency / time.Duration(testAttempts)
    fmt.Printf("\nAverage RTT (over %d attempts): %v\n", testAttempts, averageLatency)
}
