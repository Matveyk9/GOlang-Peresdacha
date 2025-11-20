package main

import (
	"encoding/json"
	"fmt"
	"log"
	"net/http"
)

type User struct {
	ID   int    `json:"id"`
	Name string `json:"name"`
}

var users = []User{
	{ID: 1, Name: "Alice"},
	{ID: 2, Name: "Bob"},
}

func getUsers(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	if err := json.NewEncoder(w).Encode(users); err != nil {
		http.Error(w, fmt.Sprintf("Ошибка кодирования JSON: %v", err), http.StatusInternalServerError)
	}
}

func getUser(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")

	// В реальном случае парсили бы id из URL
	// Здесь просто пример для пользователя с ID=1
	for _, u := range users {
		if u.ID == 1 {
			json.NewEncoder(w).Encode(u)
			return
		}
	}

	http.Error(w, "Пользователь не найден", http.StatusNotFound)
}

func main() {
	// Роутинг
	http.HandleFunc("/users", getUsers)
	http.HandleFunc("/users/1", getUser) 

	port := 8080
	fmt.Printf("Сервер запущен на http://localhost:%d\n", port)
	if err := http.ListenAndServe(fmt.Sprintf(":%d", port), nil); err != nil {
		log.Fatalf("Не удалось запустить сервер: %v", err)
	}
}
