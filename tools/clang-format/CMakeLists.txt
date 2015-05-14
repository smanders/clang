set(LLVM_LINK_COMPONENTS support)

include(xpfunmac OPTIONAL)
if(COMMAND xpGetNumBits)
  xpGetNumBits(NUMBITS)
else()
  set(NUMBITS)
endif()

add_clang_executable(clang-format
  ClangFormat.cpp
  )

target_link_libraries(clang-format
  clangBasic
  clangFormat
  clangRewrite
  clangToolingCore
  )

install(TARGETS clang-format EXPORT clang-format-targets RUNTIME DESTINATION bin${NUMBITS})
install(EXPORT clang-format-targets DESTINATION bin${NUMBITS}/cmake)
install(PROGRAMS clang-format-bbedit.applescript DESTINATION share/clang)
install(PROGRAMS clang-format-diff.py DESTINATION share/clang)
install(PROGRAMS clang-format-sublime.py DESTINATION share/clang)
install(PROGRAMS clang-format.el DESTINATION share/clang)
install(PROGRAMS clang-format.py DESTINATION share/clang)
install(PROGRAMS git-clang-format DESTINATION bin${NUMBITS})
