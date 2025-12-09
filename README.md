# Network-Latency-Optimization-Utility
// LatencyTester.go

// LatencyTester.go (Updated Implementation)

package main

import (
	"fmt"
	"time"
)

// Define the assumed address of the game server
const gameServerAddress = "game.competitivebattle.net:8080"
const testAttempts = 5
// NEW: Critical threshold for competitive play (e.g., 80 milliseconds)
const criticalLatencyThreshold = 80 * time.Millisecond 

// Simulate a network request and measure RTT latency
func measureLatency(address string) (time.Duration, error) {
    // Simulate network delay (now with potential for higher latency)
    delay := time.Duration(10 + (time.Now().UnixNano() % 100)) * time.Millisecond 
    
    // Occasionally simulate a high latency spike for testing the threshold logic
    if time.Now().Second() % 10 == 0 { 
        delay += 150 * time.Millisecond 
    }
    
    start := time.Now()
    time.Sleep(delay)
    rtt := time.Since(start)
    return rtt, nil
}

// NEW: Function to recommend strategy based on latency
func recommendStrategy(latency time.Duration) string {
    if latency < 20*time.Millisecond {
        return "HIGH_PERFORMANCE_MODE (Execute Complex Predictive Models)"
    } else if latency < criticalLatencyThreshold {
        return "STANDARD_MODE (Optimized Tactical Decisions)"
    } else {
        // If latency is too high, switch to a defensive, reaction-based strategy
        return "LAG_COMPENSATION_MODE (Prioritize Simple Defensive/Reactive Moves)"
    }
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
    fmt.Printf("\n--- Network Status ---\n")
    fmt.Printf("Average RTT (over %d attempts): %v\n", testAttempts, averageLatency)
    
    // NEW: Recommend strategy based on the average latency
    fmt.Printf("Recommended Agent Strategy: %s\n", recommendStrategy(averageLatency))
}
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
