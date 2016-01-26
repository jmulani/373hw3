#include <assert.h>
#include <stdlib.h>

#include "list.h"

// Takes a valid, sorted list starting at `head` and adds the element
// `new_element` to the list. The list is sorted based on the value of the
// `index` member in ascending order. Returns a pointer to the head of the list
// after the insertion of the new element.
list_t* insert_sorted(list_t* head, list_t* new_element) {
	assert(head != NULL);

	assert(new_element != NULL);

	list_t* first = head;

	list_t* second = head->next;

	if(first->index > new_element->index)
	{
		new_element->next = head;
		head = new_element;
		return head;
	}

	while(second != NULL && second->index < new_element->index)
	{
		first = first->next;
		second = second->next;
	}


	first->next = new_element;
	new_element->next = second;
	return head;
}

// Reverses the order of the list starting at `head` and returns a pointer to
// the resulting list. You do not need to preserve the original list.
list_t* reverse(list_t* head) {
	assert(head != NULL);

	list_t* first = head;
	list_t* second = head->next;
	list_t* temp = NULL;

	head->next = NULL;

	while(second != NULL)
	{
		temp = second->next;
		second->next = first;
		first = second;
		second = temp;
	}

	head = first;

	return head;
}
