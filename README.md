# Corosive-package main

import (
	"errors"
	"fmt"
)

// Define a map to store the artists and their stock values
var artistStocks = make(map[string]int)

/**
 * Function to buy artists like stocks
 * @param {string} artist - The name of the artist
 * @param {int} quantity - The quantity of stocks to buy
 */
func buyArtistStock(artist string, quantity int) {
	// Check if the artist already exists in the artistStocks map
	if val, ok := artistStocks[artist]; ok {
		// Increase the stock value of the artist
		artistStocks[artist] = val + quantity
	} else {
		// Add the artist to the artistStocks map with the initial stock value
		artistStocks[artist] = quantity
	}

	fmt.Printf("Successfully bought %d stocks of %s\n", quantity, artist)
}

/**
 * Function to sell artists like stocks
 * @param {string} artist - The name of the artist
 * @param {int} quantity - The quantity of stocks to sell
 */
func sellArtistStock(artist string, quantity int) error {
	// Check if the artist exists in the artistStocks map
	if val, ok := artistStocks[artist]; ok {
		// Check if the quantity to sell is greater than the available stock
		if quantity > val {
			return errors.New(fmt.Sprintf("Not enough stocks of %s to sell", artist))
		}

		// Decrease the stock value of the artist
		artistStocks[artist] = val - quantity

		fmt.Printf("Successfully sold %d stocks of %s\n", quantity, artist)
		return nil
	} else {
		return errors.New(fmt.Sprintf("%s is not in the artist stocks", artist))
	}
}

/**
 * Function to get the current stock value of an artist
 * @param {string} artist - The name of the artist
 * @returns {int} - The current stock value of the artist
 */
func getArtistStockValue(artist string) int {
	// Check if the artist exists in the artistStocks map
	if val, ok := artistStocks[artist]; ok {
		return val
	} else {
		fmt.Printf("%s is not in the artist stocks\n", artist)
		return 0
	}
}

func main() {
	// Example usage
	buyArtistStock("Artist1", 10)
	buyArtistStock("Artist2", 5)
	sellArtistStock("Artist1", 3)
	fmt.Println(getArtistStockValue("Artist1"))
	fmt.Println(getArtistStockValue("Artist2"))
}
