package coverage

import (
	"os"
	"reflect"
	"testing"
	"time"
)

func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// TestPeopleLen tests the Len method of the People type.
// Len method should return the length of the slice.
func TestPeopleLen(t *testing.T) {
	tests := []struct {
		name string
		p    People
		want int
	}{
		{
			name: "Empty People slice",
			p:    People{},
			want: 0,
		},
		{
			name: "One person",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)}},
			want: 1,
		},
		{
			name: "Two people",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Jane", "Doe", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)}},
			want: 2,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := tt.p.Len(); got != tt.want {
				t.Errorf("People.Len() = %v, want %v", got, tt.want)
			}
		})
	}
}

// TestPeople_Less tests the Less method of the People type.
// Less is used to sort the people in the People slice.
// The Less method should return true if the person with index i
// should come before the person with index j in the sorted slice, false otherwise.
func TestPeople_Less(t *testing.T) {
	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
		want bool
	}{
		{
			name: "Two people with the same birth date and first name",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"John", "Mactavish", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{0, 1},
			want: true,
		},
		{
			name: "Two people with the same birth date and last name",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Catherine", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{0, 1},
			want: false,
		},
		{
			name: "Two people with the same birth date and first name and last name",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{0, 1},
			want: false,
		},
		{
			name: "Two people with different birth dates. The first person is elder",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{0, 1},
			want: false,
		},
		{
			name: "Two people with different birth dates. The second person is younger",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{1, 0},
			want: true,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := tt.p.Less(tt.args.i, tt.args.j); got != tt.want {
				t.Errorf("People.Less() = %v, want %v", got, tt.want)
			}
		})
	}
}

// TestPeople_Swap tests the Swap method of the People type.
// Swap is used to swap the people with indexes i and j in the People slice.
func TestPeople_Swap(t *testing.T) {
	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
		want People
	}{
		{
			name: "Swap two people",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{0, 1},
			want: People{
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)}},
		},
		{
			name: "Do nothing if the indexes are the same",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{0, 0},
			want: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)}},
		},
		{
			name: "Swap two people. The indexes are swapped",
			p: People{
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)}},
			args: args{1, 0},
			want: People{
				Person{
					"Catherine", "MacTavish", time.Date(1990, 5, 1, 0, 0, 0, 0, time.UTC)},
				Person{
					"John", "Doe", time.Date(1985, 10, 1, 0, 0, 0, 0, time.UTC)}},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			tt.p.Swap(tt.args.i, tt.args.j)
		})
	}
}

// TestNew tests the initialization of new instance of Matrix struct.
func TestNew(t *testing.T) {
	type args struct {
		str string
	}
	tests := []struct {
		name    string
		args    args
		want    *Matrix
		wantErr bool
	}{
		{
			name: "Create a matrix from a string",
			args: args{
				str: "1 2 3\n4 5 6\n7 8 9"},
			want: &Matrix{
				rows: 3,
				cols: 3,
				data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9}},
			wantErr: false,
		},
		{
			name: "Create a matrix from a string with a new line at the end",
			args: args{
				str: "1 2 3\n4 5 6\n7 8 9\n"},
			want:    nil,
			wantErr: true,
		},
		{
			name: "Matrix is nil if the string is empty",
			args: args{
				str: ""},
			want:    nil,
			wantErr: true,
		},
		{
			name: "Matrix is not possible to create if columns are not the same as rows",
			args: args{
				str: "1 2 3\n4 5 6\n7 8 9\n10"},
			want:    nil,
			wantErr: true,
		},
		{
			name: "Matrix is not possible to create if the string is not a matrix",
			args: args{
				str: "some weird string"},
			want:    nil,
			wantErr: true,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := New(tt.args.str)
			if (err != nil) != tt.wantErr {
				t.Errorf("New() error = %v, wantErr %v", err, tt.wantErr)
				return
			}
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("New() = %v, want %v", got, tt.want)
			}
		})
	}
}

// TestMatrix_Rows tests the Rows method of the Matrix type.
func TestMatrix_Rows(t *testing.T) {
	type fields struct {
		rows int
		cols int
		data []int
	}
	tests := []struct {
		name   string
		fields fields
		want   [][]int
	}{
		{
			name: "Create a 2x2 matrix",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			want: [][]int{
				{1, 2},
				{3, 4}},
		},
		{
			name: "Create a 3x3 matrix",
			fields: fields{
				rows: 3,
				cols: 3,
				data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9}},
			want: [][]int{
				{1, 2, 3},
				{4, 5, 6},
				{7, 8, 9}},
		},
		{
			name: "Create a 4x4 matrix",
			fields: fields{
				rows: 4,
				cols: 4,
				data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16}},
			want: [][]int{
				{1, 2, 3, 4},
				{5, 6, 7, 8},
				{9, 10, 11, 12},
				{13, 14, 15, 16}},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := Matrix{
				rows: tt.fields.rows,
				cols: tt.fields.cols,
				data: tt.fields.data,
			}
			if got := m.Rows(); !reflect.DeepEqual(got, tt.want) {
				t.Errorf("Matrix.Rows() = %v, want %v", got, tt.want)
			}
		})
	}
}

// TestMatrix_Cols tests the Cols method of the Matrix type.
// Cols method is the same as Rows method, except that it returns the matrix represented by the columns.
func TestMatrix_Cols(t *testing.T) {
	type fields struct {
		rows int
		cols int
		data []int
	}
	tests := []struct {
		name   string
		fields fields
		want   [][]int
	}{
		{
			name: "Create a 2x2 matrix",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			want: [][]int{
				{1, 3},
				{2, 4}},
		},
		{
			name: "Create a 3x3 matrix",
			fields: fields{
				rows: 3,
				cols: 3,
				data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9}},
			want: [][]int{
				{1, 4, 7},
				{2, 5, 8},
				{3, 6, 9}},
		},
		{
			name: "Create a 4x4 matrix",
			fields: fields{
				rows: 4,
				cols: 4,
				data: []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16}},
			want: [][]int{
				{1, 5, 9, 13},
				{2, 6, 10, 14},
				{3, 7, 11, 15},
				{4, 8, 12, 16}},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := Matrix{
				rows: tt.fields.rows,
				cols: tt.fields.cols,
				data: tt.fields.data,
			}
			if got := m.Cols(); !reflect.DeepEqual(got, tt.want) {
				t.Errorf("Matrix.Cols() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestMatrix_Set(t *testing.T) {
	type fields struct {
		rows int
		cols int
		data []int
	}
	type args struct {
		row   int
		col   int
		value int
	}
	tests := []struct {
		name   string
		fields fields
		args   args
		want   bool
	}{
		{
			name: "Set value to a matrix",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			args: args{
				row:   1,
				col:   1,
				value: 5},
			want: true,
		},
		{
			name: "Set value to a matrix with invalid row",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			args: args{
				row:   3,
				col:   1,
				value: 5},
			want: false,
		},
		{
			name: "Set value to a matrix with invalid column",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			args: args{
				row:   1,
				col:   3,
				value: 5},
			want: false,
		},
		{
			name: "Set value to a matrix with invalid row and column",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			args: args{
				row:   3,
				col:   3,
				value: 5},
			want: false,
		},
		{
			name: "Set value to a matrix with negative row",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			args: args{
				row:   -1,
				col:   1,
				value: 5},
			want: false,
		},
		{
			name: "Set value to a matrix with negative column",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			args: args{
				row:   1,
				col:   -1,
				value: 5},
			want: false,
		},
		{
			name: "Set value to a matrix with negative row and column",
			fields: fields{
				rows: 2,
				cols: 2,
				data: []int{1, 2, 3, 4}},
			args: args{
				row:   -1,
				col:   -1,
				value: 5},
			want: false,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			m := &Matrix{
				rows: tt.fields.rows,
				cols: tt.fields.cols,
				data: tt.fields.data,
			}
			if got := m.Set(tt.args.row, tt.args.col, tt.args.value); got != tt.want {
				t.Errorf("Matrix.Set() = %v, want %v", got, tt.want)
			}
		})
	}
}
