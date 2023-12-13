To create a service that provides a value and allows you to access and modify it from anywhere in your Angular components, you can use a combination of a private BehaviorSubject and a public Observable. Here's how you can do it:

1. Create a service with a BehaviorSubject:

```typescript
import { Injectable } from "@angular/core";
import { BehaviorSubject, Observable } from "rxjs";

@Injectable({
	providedIn: "root", // Make sure the service is available as a singleton across the application
})
export class DataService {
	private dataSubject: BehaviorSubject<string> = new BehaviorSubject<string>(
		"Initial Value"
	);

	setData(newValue: string): void {
		this.dataSubject.next(newValue);
	}

	getData(): Observable<string> {
		return this.dataSubject.asObservable();
	}
}
```

In this example, the `DataService` contains a private `dataSubject`, which is a BehaviorSubject initialized with the initial value 'Initial Value'. The service provides two methods: `setData(newValue: string)` to set the new value and `getData(): Observable<string>` to get the observable that emits the current value.

2. Access the service in your components:

```typescript
import { Component, OnDestroy } from "@angular/core";
import { DataService } from "./data.service";
import { Subscription } from "rxjs";

@Component({
	selector: "app-your-component",
	template: `
		<div>
			Current Value: {{ currentValue }}
			<button (click)="updateValue()">Update Value</button>
		</div>
	`,
})
export class YourComponent implements OnDestroy {
	currentValue: string;
	private dataSubscription: Subscription;

	constructor(private dataService: DataService) {
		this.dataSubscription = this.dataService.getData().subscribe((value) => {
			this.currentValue = value;
		});
	}

	updateValue(): void {
		this.dataService.setData("New Value");
	}

	ngOnDestroy(): void {
		this.dataSubscription.unsubscribe();
	}
}
```

In this example, `YourComponent` subscribes to the `getData()` observable from the `DataService` in its constructor. The subscription updates the `currentValue` property whenever the value in the service changes.

The `updateValue()` method allows you to change the value using the `setData()` method from the service.

Remember to provide the `DataService` at the root level (using `providedIn: 'root'`) or in a module to make sure it's available as a singleton throughout the application.

With this setup, you can use the `DataService` to store and share data across different components in your Angular application.
