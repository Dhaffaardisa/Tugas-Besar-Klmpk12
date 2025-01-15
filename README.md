#include <stdio.h>
#include <string.h>
#define MAX_RESERVATIONS 100

typedef struct {
    char name[50];
    int User;
    int queue_number;
} Reservation;

Reservation reservations[MAX_RESERVATIONS];
int reservation_count = 0;
int next_antrian_number = 1;

void addReservation(char name[], int people);
void viewReservations();

int main() {
    int choice;
    char name[50];
    int User;

    do {
        printf("\nFast Food antrian Management System\n");
        printf("1. antrian User\n");
        printf("2. Menu\n");
        printf("3. Exit\n");
        printf("Silahkan dipilih: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("\nNama User: ");
                scanf("%s", name);
                printf("Nomor antrian: ");
                scanf("%d", &User);
                addReservation(name, User);
                break;
            case 2:
                viewReservations();
                break;
            case 3:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (choice != 3);

    return 0;
}

void addReservation(char name[], int people) {
    if (reservation_count < MAX_RESERVATIONS) {
        strcpy(reservations[reservation_count].name, name);
        reservations[reservation_count].User = people;
        reservations[reservation_count].queue_number = next_antrian_number++;
        reservation_count++;
        printf("Customer added to queue successfully!\n");
    } else {
        printf("Unable to add customer. The queue is full.\n");
    }
}

void viewReservations() {
    if (reservation_count == 0) {
        printf("No customers in the queue.\n");
    } else {
        printf("\nCurrent Queue:\n");
        for (int i = 0; i < reservation_count; i++) {
            printf("%d. Name: %s, People: %d, Queue Number: %d\n", 
                   i + 1, reservations[i].name, reservations[i].User, reservations[i].queue_number);
        }
    }
}
