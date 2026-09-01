## Insert Data into Supabase PostgreSQL

#### Create module, service, controller
```bash
nest g module employee-bd
```
```bash
nest g service employee-bd
```
```bash
nest g controller employee-bd
```
---


>#### file add koro- employees.entity.ts
#### `employees.entity.ts`
```bash
import { Entity, PrimaryGeneratedColumn, Column } from "typeorm";


@Entity()
export class Employee {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @Column()
    position: string;

    @Column()
    department: string;

    @Column()
    salary: number;
}
```
---
