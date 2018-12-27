Conform Popup
=============
confirm popup dialog to get user's choice.

```ts
import { AppConfirmModule } from '@ngx-starter-kit/app-confirm'
import { AppConfirmService } from '@ngx-starter-kit/app-confirm';

constructor(private confirmService: AppConfirmService) {}


delete(item: Account) {
  return this.confirmService.confirm('Confirm', `Delete ${item.first_name} ${item.last_name}?`).pipe(
    filter(confirmed => confirmed === true),
    mergeMap(_ => super.delete(item)),
    tap(_ => {
      this.snack.open('Member Deleted!', 'OK', { duration: 5000 });
      this.store.dispatch(new Navigate([`/dashboard/grid/crud-table`]));
    }),
    catchError(error => {
      this.snack.open(error, 'OK', { duration: 10000 });
      return throwError('Ignore Me!');
    }),
  );
}

```