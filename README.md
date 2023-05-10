.global _start

  .section .text
_start: 
   xor %r10,%r10
   xor %r11,%r11
   xor %r12,%r12
   xor %r13,%r13
   xor %r14,%r14
   xor %r15,%r15
   movq Source(%rip),%rsi
   movq head(%rip),%rdi 
   testq %rdi,%rdi
   je end_HW1
   movl (Value),%eax
   cmpq %rsi,%rdi
   je find_val_prev_HW1
  

loop_HW1: 
   cmp (%rdi),%eax
   je find_source_prev_HW1
   movq 4(%rdi),%rdi
   cmp $0,%rdi
   je end_HW1 
   jmp loop_HW1 


find_source_prev_HW1:
    cmp %rdi,%rsi
    je end_HW1
    movq head(%rip),%r10
    cmpq %r10,%rsi
    je find_val_prev_HW1
prevs_loop:
    cmp 4(%r10),%rsi
    je find_val_prev_HW1
    movq 4(%r10),%r10
    jmp prevs_loop

find_val_prev_HW1:
     movq head(%rip),%r11
     cmpq %r11,%rdi
     je swap_HW1
prevv_loop:
     cmp 4(%r11),%rdi
    je swap_HW1
    movq 4(%r11),%r11
    jmp prevv_loop


   

swap_HW1: 

   cmp 4(%rsi),%rdi
   je sticked1_HW1
   cmp 4(%rdi),%rsi
   je sticked2_HW1
   movq 4(%rsi),%r12
   movq 4(%rdi),%r13
   movq %rdi,4(%r10)
   movq %rsi,4(%r11) 
   movq %r12,4(%rdi)
   movq %r13,4(%rsi)
   jmp end_HW1

sticked1_HW1: 
   
   movq 4(%r10),%r12  
   movq 4(%r11),%r13
   movq %r13,4(%r10)  
   movq 4(%r13),%r15
   movq %r15,4(%r12) 
   movq %r12,4(%r13)
  
   
   jmp end_HW1
   

sticked2_HW1: 
  
   movq 4(%r11),%r12  
   movq 4(%r10),%r13
   movq %r13,4(%r11)  
   movq 4(%r13),%r15
   movq %r12,4(%r13)
   movq %r15,4(%r12) 
   jmp end_HW1
   
   
end_HW1: 
  
